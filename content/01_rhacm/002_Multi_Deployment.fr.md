---
title: "Déploiement et gestion d'une application"
draft: false
weight: 3
---


## Contexte

Notre application **airports-frontend** est un frontend écrit en [quarkus](https://quarkus.io) et affichant des aéroports ainsi que des avions se déplaçant entre les aéroports. Néanmoins dans le cadre de ce workshop, nous ne nous occuperons ici que du frontend et nous ne verrons pas les avions se déplacer.

Notre application étant de plus en plus critique, il a été décidé de la déployer sur 2 clusters différents.


## Objectif de l'exercice

L'objectif de cet exercice est de déployer notre application **airports-frontend** en mode multi-cluster en utilisant les mécanismes d'OpenShit Advanced Cluster Managment.

## Étapes de l'exercice

Depuis le cluster Hub OpenShift, accéder à l'interface d'ACM.
Pour cela, en haut de l'écran, cliquer sur **local-cluster** puis **All Clusters** :

![ACM Console](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)


Aller ensuite dans la partie **Applications** 

![ACM Applications](/OPP-2023-lab-instruction.github.io/images/acm-applications.png)


## A vous de jouer 

1 - __Déploiement sur le cluster de développement__
- Créer une application de type **Subscription**
- Son nom sera **<VOTRE_USER>-airports-frontend**
- Son namespace sera **<VOTRE_USER>-airports-frontend**
- Repository **Git** basé sur [airports-frontend](https://github.com/workshop-opp/airports-frontend.git)
- Branch : **main**
- Path : **k8s**
- Déployer l'application sur le Cluster sets **default** et choisissez 1 label identifiant UNIQUEMENT notre cluster de développement (astuce : vous pouvez trouver l'ensemble des labels de chaque cluster dans le menu Infrastructure)
- Vérifier dans l'onglet **Topology** que l'application s'est bien déplpoyée sur le bon cluster (vous pouvez également vous connecter à la console OpenShift du cluster de Dev et vérifier que le nouveau namespace contient votre application )

## Solution

{{%expand "Solution guidée" %}}


{{% /expand%}}


2 - __Déploiement sur le cluster de Dev et de Prod simultanément__
- Retourner sur votre application **<VOTRE_USER>-airports-frontend**
- Editer là
- Créer une nouvelle règle de placement utilisant un label **commun** aux 2 clusters
- Oberver et vérifier que votre application est déployée sur les 2 clusters

## Solution

{{%expand "Solution guidée" %}}


{{% /expand%}}


3 - __Exercice BONUS : GitOps avec ACM__

Nous allons observer les mécanismes GitOps offerts par ACM : pour ce faire, il vous faudra **OBLIGATOIREMENT** un compte GitHub.
- Connecter vous avec votre login personnel à [GitHub](https://github.com)
- Effectuez un fork du repository https://github.com/workshop-opp/airports-frontend
- Modifier l'application **<VOTRE_USER>-airports-frontend** pour utiliser le repository que vous venez de forker (https://github.com/<VOTRE_USER_GITHUB/airports-frontend)
- Modifier le nombre de replicas dans le fichier `k8s/deployment.yaml` sur le repository de VOTRE compte
- Oberver le changement du nombre de PODs déployés

{{%expand "Solution guidée" %}}


{{% /expand%}}