---
title: "CVE Management"
draft: false
weight: 2
---

## Contexte :

L'équipe de sécurité informatique a reçu une alerte concernant une nouvelle vulnérabilité critique (CVE) qui pourrait avoir un impact important sur les systèmes. Cette CVE affecte plusieurs  applications. Pour prévenir toute exploitation potentielle de cette vulnérabilité, il est crucial de détecter et d'empêcher tout nouveau déploiement d'application susceptible de la contenir.

## Objectif de l'exercice :

L'objectif principal est de mettre en place une politique de sécurité qui bloque tout déploiement d'application contenant la CVE identifiée sur le cluster concerné. Cette politique doit être automatisée pour prévenir tout risque de déploiement involontaire d'une application vulnérable.

## Étapes de l’exercice :

Acceder a l'interface RHACS et rendez vous dans la section Vulnerability Management. Cette interface vous donne une visibilite sur l'ensemble des images appartenant a votre scope.

## A vous de jouer 

A partir de ces differents dashboard nous vous demandons de retrouver et d'exporter toutes les deployment affecte par la CVE sous le format PDF. 

Une fois cette etape realiser. Rendez vous dans Platform Configuration > Policy Management et cliquez sur Create Policy. Vous completerez le formulaire de sorte que toutes les images portant la CVE `CVE X` soit bloque au Stage Build et Deploy avec une methode de reponse de type Inform and Enforce.

## Solution


{{%expand "Solution: Exporter la liste des Deployment touche par la CVE CVE-X" %}}

Cliquez sur Application & Infrastructure puis cliquez sur Deployment. Dans la barre de filtre ecrivez CVE puis le numero de notre CVE

Vous verrez alors apparaitre tout les deployment concerner par notre vulnerabilite. Cliquez alors sur Export en haut a gauche pour exporter un PDF contenant l'ensemble des informations.

{{% /expand%}}

{{%expand "Solution: Creation de la Policy" %}}

{{% /expand%}}



