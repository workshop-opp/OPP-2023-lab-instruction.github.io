---
title: "DevSecOps Pipeline"
draft: false
weight: 4
---


Dans cette partie, nous allons voir comment RHACS peut totalement s'intègrer dans une approche DevSecOps.


## Contexte


L'équipe de développeur utilise une pipeline pour git clone un dépôt distant, build l'image et déployer l'application sur le cluster.  
Entre l'étape du build et du déploiement, nous avons 2 étapes parallèles : image-scan, image-check.
Ces étapes permet à RHACS de chercher les vulnérabilités présentes dans l'application.
RHACS vous informe qu'une CVE est présente sur l'application qui est déployé via la pipeline.

## Objectifs de l'exercice

L'objectif est de trouver la CVE qui est présente dans l'application est bloqué tout nouveau déploiment.

## Etapes de l'exercice
Pour parvenir à l'objectif de l'activité, vous devez :
- Lancer la pipeline pour permettre au déploiement de l'application
- trouver la CVE présente dans l'application
- Modifier la policy correspondante à la policy pour bloquer tout nouveau déploiement
- Relancer la pipeline


## A vous de jouer

## Solution


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






