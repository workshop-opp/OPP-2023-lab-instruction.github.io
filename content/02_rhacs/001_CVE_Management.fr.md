---
title: "Gestion des CVE"
draft: false
weight: 2
---

## Contexte

L'équipe de sécurité informatique a reçu une alerte concernant une nouvelle vulnérabilité critique (CVE) qui pourrait avoir un impact important sur les systèmes. Cette CVE affecte plusieurs  applications. Pour prévenir toute exploitation potentielle de cette vulnérabilité, il est crucial de détecter et d'empêcher tout nouveau déploiement d'application susceptible de la contenir.

## Objectif de l'exercice

L'objectif principal est de mettre en place une politique de sécurité qui bloque tout déploiement d'application contenant la CVE identifiée sur le cluster concerné. Cette politique doit être automatisée pour prévenir tout risque de déploiement involontaire d'une application vulnérable.

## Étapes de l’exercice

Acceder à l'interface RHACS et rendez vous dans la section Vulnerability Management. Cette interface vous donne une visibilite sur l'ensemble des images appartenant à votre scope.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/dashboard-vulnerability-management.png)


## A vous de jouer 

A partir de ces différents tableau de bord nous vous demandons de retrouver et d'exporter tous les déploiements concernés par les CVE au format PDF.

Une fois cette étape terminée, accédez à Configuration de la plateforme > Gestion des stratégies et cliquez sur Créer une policy. Vous remplirez le formulaire afin que toutes les images portant le CVE `CVE-2022-32207` soient bloquées lors des Stage Build and Deploy avec une méthode `Inform and Enforce`.

La policy doit répondre au critère suivant :

| Parameters | Value |
|----------|----------|
| Name | **policy-<VOTRE_VILLE>** |
| Categories | Vulnerability Management |
| Lifecycle stages| Build and Deploy |
| Response method | Inform and enforce |
| Restrict-by-scope | **<VOTRE_VILLE>-ns** |
| Cluster-scope | local-cluster |

## Solution


{{%expand "Solution: Exporter la liste des déploiements concernés par le CVE `CVE-2022-32207` " %}}

Cliquez sur Application et infrastructure, puis sur Deployment. 

![Dashboard](/OPP-2023-lab-instruction.github.io/images/dashboard.png)

Dans la barre de filtre écrivez CVE puis le numéro de la CVE.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/peloton.png)

Vous verrez alors apparaître tous les déploiements concernés par notre vulnérabilité. Cliquez ensuite sur Exporter en haut à droite pour exporter un PDF contenant toutes les informations.

{{% /expand%}}

{{%expand "Solution : Création de la Policy" %}}

![Policy-1](/OPP-2023-lab-instruction.github.io/images/create-policy-step-1.png)

![Policy-2](/OPP-2023-lab-instruction.github.io/images/create-policy-step-2.png)

![Policy-3](/OPP-2023-lab-instruction.github.io/images/create-policy-step-3.png)

![Policy-4](/OPP-2023-lab-instruction.github.io/images/create-policy-step-4.png)

TODO: Add manifest to validate

{{% /expand%}}



