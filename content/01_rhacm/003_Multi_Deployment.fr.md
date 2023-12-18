---
title: "Déploiement et gestion d'une application"
draft: false
weight: 3
---


## Contexte

Notre application **airports-frontend** est un frontend écrit en [quarkus](https://quarkus.io) et affichant des aéroports ainsi que des avions se déplaçant entre les aéroports. Néanmoins dans le cadre de ce workshop, nous ne nous occuperons ici que du frontend et nous ne verrons pas les avions se déplacer.

Notre application étant de plus en plus critique, il a été décidé de la déployer sur 2 clusters différents.


## Objectif de l'exercice

L'objectif de cet exercice est de déployer notre application **airports-frontend** en mode multi-cluster en utilisant les mécanismes d'OpenShit Advanced Cluster Management.

## Étapes de l'exercice

Depuis le cluster Hub OpenShift, accéder à l'interface d'ACM.
Pour cela, en haut de l'écran, cliquer sur **local-cluster** puis **All Clusters** :

![ACM Console](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)


Aller ensuite dans la partie **Applications** 

![ACM Applications](/OPP-2023-lab-instruction.github.io/images/acm-applications.png)


## A vous de jouer !


#### Exercice 1 : 
__1 - Déploiement sur le cluster de développement__
- Créer une application de type **Subscription**  (le type **Application Set** nécessiterait l'installation d'ArgoCD ce qui n'est pas l'objectif ici)
- Son nom sera **<VOTRE_VILLE>-airports-frontend**
- Son namespace sera **<VOTRE_VILLE>-ns**
- Repository **Git** basé sur [https://github.com/workshop-opp/airports-frontend.git](https://github.com/workshop-opp/airports-frontend.git)
- Branch : **main**
- Path : **k8s**
- Déployer l'application sur le Cluster sets **global** et choisissez 1 label identifiant UNIQUEMENT notre cluster de développement 

{{% notice tip %}}
Astuce : vous pouvez trouver l'ensemble des labels de chaque cluster dans le menu Infrastructure
{{% /notice %}}

- Vérifier dans l'onglet **Topology** que l'application s'est bien déployée sur le bon cluster (vous pouvez également vous connecter à la console OpenShift du cluster de Dev et vérifier que le nouveau namespace contient votre application )


{{%expand "Solution Exercice 1" %}}

Remplissez le formulaire comme indiqué ci-dessous (en remplaçant `tokyo` par le nom de votre ville).

![ACM Applications step 1](/OPP-2023-lab-instruction.github.io/images/create-application-step-1.png)

Dans l'onglet Infrastructure, vous avez probablement remarqué qu'un label `environment=dev` a été appliquée au cluster de développement. C'est celui que nous allons utiliser.

![ACM Applications step 2](/OPP-2023-lab-instruction.github.io/images/create-application-part-2.png)

Cliquez ensuite sur Créer en haut à droite.

Vous devez observer que le déploiement de votre application fonctionne bien dans la vue topologie.

![Topology part 1 ](/OPP-2023-lab-instruction.github.io/images/topology-part1.png)

En cliquant sur route puis sur `launch route url` , vous devriez voir l'application ci-dessous.

![Airport application sno dev](/OPP-2023-lab-instruction.github.io/images/airport-application-sno-dev.png)

{{% notice note %}}
Vous remarquerez dans l'URL que l'application a été déployée sur sno-dev comme prévu.
{{% /notice %}}


{{% /expand%}}

#### Exercice 2 :
__2 - Déploiement sur le cluster de Dev et de Prod simultanément__

- Retourner sur votre application **<VOTRE_VILLE>-airports-frontend**
- Editer là
- Créer une nouvelle règle de placement utilisant un label **commun** aux 2 clusters
- Oberver et vérifier que votre application est déployée sur les 2 clusters

{{%expand "Solution Exercice 2" %}}

Dans la section application, recherchez votre application créée précédemment puis cliquez dessus.

![Search application](/OPP-2023-lab-instruction.github.io/images/application-search.png)

Cliquez sur Actions > Modifier l'application en haut à droite. Ouvrez ensuite la section Sélectionner les clusters pour le déploiement d'applications et cliquez sur `Deploy application resources on clusters with all specified labels`. Dans ClusterSet, utilisez à nouveau global et dans l'étiquette, sélectionnez deploy=acm.



![deploy dev and prod](/OPP-2023-lab-instruction.github.io/images/deploy-dev-and-prod.png)

Dans la vue topologique, vous devriez maintenant voir que l'application a été déployée sur les clusters de développement et de production.

![Topology part 2](/OPP-2023-lab-instruction.github.io/images/topology-part2.png)



{{% /expand%}}

#### Exercice 3 (Bonus) :
__3 - GitOps avec ACM__

Nous allons observer les mécanismes GitOps offerts par ACM : pour ce faire, il vous faudra **OBLIGATOIREMENT** un compte GitHub.
- Connecter vous avec votre login personnel à [https://github.com](https://github.com)
- Effectuez un fork du repository https://github.com/workshop-opp/airports-frontend
- Modifier l'application **<VOTRE_USER>-airports-frontend** pour utiliser le repository que vous venez de forker (https://github.com/<VOTRE_USER_GITHUB/airports-frontend)
- Modifier le nombre de replicas à 2 (au lieu de 1) dans le fichier `k8s/deployment.yaml` sur le repository de VOTRE compte
- Enregistrer et commiter votre code
- Oberver le changement du nombre de PODs déployés dans ACM (il peut se passer quelques temps avant le changement)

