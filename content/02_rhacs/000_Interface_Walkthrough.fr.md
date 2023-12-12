---
title: "Navigation dans l'interface"
draft: false
weight: 1
---


A travers cette activité, nous verrons rapidement les principales fonctionnalités de Red Hat Advanced Cluster Security

## Connexion à rhacs

Pour accéder à rhacs, cliquez sur le path menu en haut à droite et cliquez sur `Red Hat Advanced Cluster Security`.

![RHACS connexion](/OPP-2023-lab-instruction.github.io/images/rhacs-connection.png)

Selectionner atelier-opp comme fournisseur d'authentification. Puis cliquez sur login.

![Login connexion](/OPP-2023-lab-instruction.github.io/images/login-workshop-opp.png)

 Authentifiez-vous avec votre utilisateur/mot de passe fourni par l'instructeur.


## Gestion des vulnérabilités

La gestion des vulnérabilités fournit un dashboard où se trouve des informations importantes sur les application déployés sur le cluster. On y trouve principalement les vulnérabilités (CVE comprises), lesquelles sont les plus répandues ou les plus récentes, d'où proviennent les images Docker utilisés. Le dashboard fournit aussi les vulnérabilités présentes au sein du cluster.


![Vulnerabilités](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

 RHACS peut scanner les images deployées et s'intègre à vos registry. RHACS fournit également une prise en charge étendue des scanners tiers tels que Anchore, Red Hat Quay, Clair et Tenable pour compléter vos outils de scan d'images existants.


## Gestion des risques


Jetons un coup d'œil à la vue Risques, où nous allons au-delà des bases des vulnérabilités pour comprendre comment la configuration du déploiement et l'activité d'exécution affectent la probabilité qu'un exploit se produise.


![Risk](/OPP-2023-lab-instruction.github.io/images/risk.png)


Cette liste affiche les déploiements, dans tous les clusters et namespace, classés par priorité de risque.
Le risque est calculé selon l'activité de l'application, son exposition, le nombre de déploiements et les CVE présentes.
La vue est classé par odre de priorité.
Ainsi, cette fonctionnalité permettra de concentrer vos efforts sur les déploiemments qui présente le plus de risques.



## Netwok Graph

Le Network Graph est à la fois une vue des flux, et un générateur de NetworkPolicy.


![Network](/OPP-2023-lab-instruction.github.io/images/network.png)


Network Graph est une fonctionnalités de visualisation des déploiements présent sur vos namespaces.
Ainsi, cette fonctionnalité vous présente sous forme de diagramme de flux, les différentes connexion existantes sur vos différents pods.
Sur la base du diagramme vous pourrez prendre des décisions, concernant l'ajout ou la suppression des flux.
Le point fort du Network Graph est que RHACS peut vous génerer des network policies afin de mieux protèger et cloisoner vos flux de connexion.

## Violations

La section Violations est une fonctionnalité qui se présente sous forme d'un registre qui enregistre tous les moments spécifiques où une policy créée par l'équipe sécurité n'a pas été respecté dans votre cluster.

Ce registre vous permet d'un simple coup d'oeil, de voir les violations de policy présentes sur votre cluster en filtrant plusieurs informations tel que :
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

Le Compliance Operator vous fournit un dashboard qui permet d'accèder à des métriques définit pour voir l'état de conformité exigé dans certains domaines d'activités comme le domaine bancaire et médicale.
Le Compliance Operator évalue à la fois les ressources de l'API Kubernetes et les ressource d'Openshift, ainsi que les nœuds s'exécutant sur le cluster.
Cette fonctionnalité utilise OpenSCAP, un outil certifié NIST, pour analyser et appliquer les politiques de sécurité fournies par le contenu.



Cliquez sur « Analyse de l'environnement »


![Compliance_Operator](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Gestion de la configuration

Configuration Management, fournit une gestion de configuration efficace qui combine toutes les entités sur une seule page. Il rassemble des informations sur tous vos clusters, namespaces, nœuds, déploiements, images, secrets, utilisateurs, groupes, comptes de service et rôles dans une seule vue, vous aidant à visualiser différentes entités et les connexions entre elles.


## Gestion des politiques

Avec la gestion des politiques, RHACS vous permet d'utiliser des politiques de sécurité prêtes à l'emploi et de définir des politiques multifacteurs personnalisées pour votre environnement de conteneurs.
La configuration de ces stratégies vous permet d'empêcher automatiquement les déploiements de services à haut risque dans votre environnement et de répondre aux incidents de sécurité d'exécution.


![Policy](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


Toutes les politiques fournies avec le produit sont conçues dans le but de fournir des mesures correctives ciblées qui améliorent le renforcement de la sécurité.

Vous verrez que cette liste contient de nombreuses politiques sur le build et le déploiement pour détecter les erreurs de configuration (par exemple dans un pipeline), mais également des politiques d'exécution qui renvoient à des recommandations de renforcement spécifiques.



