---
title: "DevSecOps Pipeline"
draft: false
weight: 4
---


Dans cette partie, nous allons voir comment RHACS peut totalement s'intègrer dans une approche DevSecOps.


## Contexte


L'équipe de développement utilise une pipeline pour  cloner un dépôt distant, build l'image et déployer l'application sur le cluster.  
Entre l'étape du build et du déploiement, nous avons 2 étapes parallèles : image-scan, image-check.
Ces étapes permettent à RHACS de chercher les vulnérabilités présentes dans l'application.

## Objectif de l'exercice

L'objectif est de réaliser comment s'intégre RHACS dans une pipeline.



## Etapes de l'exercice

Pour commencer,allez sur le cluster hub, assurez-vous d'être dans **local-cluster**

![ACM Console](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)

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



## A vous de jouer



## Solution

{{%expand "Solution: Exporter la liste des Deployment touche par la CVE `CVE-2022-32207` " %}}



Dans Openshift Pipelines :
- Cliquer sur "START"
- Suivez les étapes d'avancement du pipeline

![Pipeline](/OPP-2023-lab-instruction.github.io/images/pipeline_1.png)



Comme vous pouvez le voir, le déploiement s'est déroulé sans problème.

Pour trouver la CVE correspondante au déploiement, aller sur le dashboard de RHACS et plus précisement dans la section Violations.


![Violations](/OPP-2023-lab-instruction.github.io/images/pipeline_2.png)

A la 1ère ligne, vous pouvez la policy pillow_policy qui a bloqué le déploiement de notre application (selon le nom de votre namespace).
Vous pouvez cliquer sur la policy pour plus de détail.
Pour informationc cette CVE concerne pillow, une librairie python qui permet de manipuler des images.
Cette CVE existe uniquement sur la version 9.5.0 de pilow, mais elle n'est plus présente sur la version la plus récente.

Pour bloquer tout nouveau déploiement :

Suivez les étapes :

- Cliquez sur Platform Configuration
- Policy Management
- Cliquez sur la barre de recherche "Filter policies", sélectionner "Policy"
- Tapez "pillow_policy", il s'agit de la policy qui ordonne le blocage du déploiement de notre application.
- Cliquer sur la policy
- en haut à gauche, cliquez sur Actions, puis edit policy.
- Allez directement à section 2 : Policy Behavior

![policy](/OPP-2023-lab-instruction.github.io/images/pipeline_3.png)

Dans la section "Response method" comme ci dessus, "inform" est coché.

- Cochez "inform and enforce"
- Cliquez sur Next jusqu'à qu'on vont proposer de sauvegarder la policy.
- Sauvegarder les modifications


Maintenant, retournez sur votre pipeline et relancez un run.

Comme vous pouvez le voir, l'application n'est pas deployé sur le cluster, car RHACS bloque le déploiement.


{{% /expand%}}



