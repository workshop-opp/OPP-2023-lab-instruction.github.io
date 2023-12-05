---
title: "Interface Walkthrough"
draft: false
weight: 1
---


A travers les pages suivantes, nous verrons rapidement les principales fonctionnalités de Red Hat Advanced Cluster Security


## Gestion des vulnérabilités

La gestion des vulnérabilités fournit un dashboard ou se trouve des informations importantes sur les application déployés sur le cluster. On y trouve principalement les vulnérabilités (CVE comprises), lesquelles sont les plus répandues ou les plus récentes, d'où proviennent les images Docker utilisés. Le dashboard fournit aussi les vulnérabilités présentes dans au sein du cluster.


![Vulnérabilités](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

Protégez vos conteneurs contre les vulnérabilités depuis le moment où les images sont créées jusqu'à leur déploiement et leur exécution. RHACS peut bloquer le déploiement des images vulnérables et s'intègre à vos registres approuvés, y compris OpenShift Container Registry, pour une application granulaire des politiques. RHACS fournit également une prise en charge étendue des scanners tiers tels que Anchore, Red Hat Quay, Clair et Tenable pour compléter vos outils de numérisation d'images existants.


## Gestion des risques


Jetons un coup d'œil à la vue Risques, où nous allons au-delà des bases des vulnérabilités pour comprendre comment la configuration du déploiement et l'activité d'exécution affectent la probabilité qu'un exploit se produise et quelle sera la réussite de ces exploits.


![Risk](/OPP-2023-lab-instruction.github.io/images/risk.png)


Cette liste affiche tous les déploiements, dans tous les clusters et namespace, classés par priorité de risque.
Le risque est calculé selon l'activité de l'application, le nombre de déploiements et les CVE présentes.
La vue est classé par odre de priorité.
Ainsi, cette fonctionnalité permettra de concentrer vos efforts sur les déploiemments qui présente le plus de risques.



## Graphique de réseau

Le Network Graph est à la fois un diagramme de flux, un diagramme de pare-feu et un générateur de règles de pare-feu.


![Network](/OPP-2023-lab-instruction.github.io/images/network.png)


Network Graph est une fonctionnalités de visualisation des déploiements présent sur vos namespaces.
Ainsi, cette fonctionnalité vous présente sous forme de diagramme de flux, les différentes connexion existantes sur vos différents pods.
Sur la base du diagramme vous pourrez prendre des décisions, concernant à ajouter ou supprimer des flux.
Le point fort de Network Graph est que RHACS peut vous génerer des network policies afin de mieux protèger et cloissoner vos flux de connexion.

## Violations

Violations est une fonctionnalité qui se présente sous forme d'un registre qui enregistre tous les moments spécifiques où une CVE ou un policy crée par l'équipe sécurité a été découvert par l'un des objets de votre cluster : images et leurs composants, déploiements, runtime.

Ce registre vous permet d'un simple coup d'oeil, les vulnérabilités présentes sur vos application en précisant plusieurs informations tel que :
- le namespace concerné
- le type : précise si la vulnérabilité ou la policy est présente sur un déployment, secret, namespace etc...
- enforced : le déploiement à été bloqué ou non
- le niveau de séverité
- la catégorie de vulnérabilité
- à quel moment la vulnérabilité ou la policy a été détecté (build,deployment,runtime)
  




![Violations](/OPP-2023-lab-instruction.github.io/images/violations1.png)

Cliquez sur n'importe quelle violation pour voir plus de détails.


![Violation2](/OPP-2023-lab-instruction.github.io/images/violation2.png)


## Compliance Operator

Compliance Operator vous fournit un dashboard qui permet d'accèder à des métriques définit pour voir l'état de conformité exigé dans certains domaines d'activités comme le domaine bancaire et médicale.
Complance Operator évalue à la fois les ressources de l'API Kubernetes et les ressource d'Openshift, ainsi que les nœuds exécutant le cluster.
L'opérateur de conformité utilise OpenSCAP, un outil certifié NIST, pour analyser et appliquer les politiques de sécurité fournies par le contenu.



Cliquez sur « Analyse de l'environnement »


![Compliance_Operator](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Gestion de la configuration

Configuration Management, fournit une gestion de configuration efficace qui combine toutes les entités sur une seule page. Il rassemble des informations sur tous vos clusters, namespaces, nœuds, déploiements, images, secrets, utilisateurs, groupes, comptes de service et rôles dans une seule vue, vous aidant à visualiser différentes entités et les connexions entre elles.


## Gestion des politiques

Avec la gestion des politiques, RHACS vous permet d'utiliser des politiques de sécurité prêtes à l'emploi et de définir des politiques multifacteurs personnalisées pour votre environnement de conteneurs.
La configuration de ces stratégies vous permet d'empêcher automatiquement les déploiements de services à haut risque dans votre environnement et de répondre aux incidents de sécurité d'exécution.


![Policy](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


Toutes les politiques fournies avec le produit sont conçues dans le but de fournir des mesures correctives ciblées qui améliorent le renforcement de la sécurité.

Vous verrez que cette liste contient de nombreuses politiques de temps de construction et de déploiement pour détecter les erreurs de configuration au début du pipeline, mais également des politiques d'exécution qui renvoient à des recommandations de renforcement spécifiques.



