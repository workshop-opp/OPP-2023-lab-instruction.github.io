---
title: "Pipeline DevSecOps"
draft: false
weight: 4
---


Dans cette partie, nous allons voir comment RHACS peut totalement s'intégrer dans une approche DevSecOps.


## Contexte


L'équipe de développement utilise une pipeline pour cloner un dépôt distant, construire l'image et déployer l'application sur le cluster.  
Entre l'étape du build et du déploiement, nous avons 2 étapes parallèles : image-scan, image-check.
Ces étapes permettent à RHACS de chercher les vulnérabilités présentes dans l'application.

## Objectif de l'exercice

L'objectif est de trouver quelle vulnérabilité critique est présente sur la pipeline.



## Etapes de l'exercice

Pour commencer, allez sur le cluster hub, assurez-vous d'être dans **local-cluster**

![Pipelines](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)

Ensuite, cliquez sur Pipelines, puis de nouveau pipelines.
Ensuite en haut à gauche dans **projects**, sélectionner le namespace **prototype**

![Pipelines](/OPP-2023-lab-instruction.github.io/images/pipeline_menu.png)


Vous disposer d'une pipeline qui s'appelle clone-build-push.

Cliquez sur **start** comme indiqué ci dessous

![Pipelines](/OPP-2023-lab-instruction.github.io/images/start_pipeline.png)

Ensuite, le menu suivant s'affiche :

Vous devez remplir les informations suivantes avant de lancer le pipeline :

- **ville** : entrer le nom de votre ville en référence à votre namespace
- **tekton-pvc** : sélectionner **PersistentVolumeClaim** puis **tekton-pvc**
- **docker-config** : sélectionner **Secret** puis **pipeline-secret**

![Pipelines](/OPP-2023-lab-instruction.github.io/images/pipeline_ville.png)


Cliquez sur **start**

## A vous de jouer

Rendez-vous dans les logs de la pipeline, pour trouver la vulnérabilité de niveau **critical**

## Solution

{{%expand "Solution" %}}

Pour trouver la vulnérabilité :

- Aller dans **Logs**
- Aller dans **image-check**
- Vous trouverez la policy critical **pillow_policy**

![Pipelines](/OPP-2023-lab-instruction.github.io/images/screen_soluce_task.png)

Donc la vulnérabilité de niveau **critical** est pillow_policy


{{% /expand%}}



