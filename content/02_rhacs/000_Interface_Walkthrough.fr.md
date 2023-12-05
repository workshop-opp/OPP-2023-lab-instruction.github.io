---
title: "Interface Walkthrough"
draft: false
weight: 1
---


A travers les pages suivantes, nous verrons rapidement les fonctionnalités disponibles sur Red Hat Advanced Cluster Security


## Gestion des vulnérabilités

L'aperçu fournit plusieurs rapports importants - où se trouvent les vulnérabilités, lesquelles sont les plus répandues ou les plus récentes, d'où proviennent mes images Docker et les vulnérabilités importantes dans OpenShift lui-même.


![Grafana](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

Protégez vos conteneurs contre les vulnérabilités depuis le moment où les images sont créées jusqu'à leur déploiement et leur exécution. RHACS peut bloquer le déploiement des images vulnérables et s'intègre à vos registres approuvés, y compris OpenShift Container Registry, pour une application granulaire des politiques. RHACS fournit également une prise en charge étendue des scanners tiers tels que Anchore, Red Hat Quay, Clair et Tenable pour compléter vos outils de numérisation d'images existants.


## Gestion des risques


Jetons un coup d'œil à la vue Risques, où nous allons au-delà des bases des vulnérabilités pour comprendre comment la configuration du déploiement et l'activité d'exécution affectent la probabilité qu'un exploit se produise et quelle sera la réussite de ces exploits.


![Grafana](/OPP-2023-lab-instruction.github.io/images/risk.png)


Cette vue de liste affiche tous les déploiements, dans tous les clusters et espaces de noms, classés par priorité de risque.

Le risque est également influencé par l'activité d'exécution - et les déploiements dont l'activité pourrait indiquer une violation en cours ont un point rouge sur la gauche. Évidemment, le premier de la liste devrait être notre premier objectif.

La réalité en matière de sécurité est qu’il n’est tout simplement pas possible de s’attaquer à toutes les sources de risque. Les organisations finissent donc par donner la priorité à leurs efforts. Nous voulons que le RHACS contribue à éclairer cette priorisation.



## Graphique de réseau

Le Network Graph est à la fois un diagramme de flux, un diagramme de pare-feu et un générateur de règles de pare-feu.


![Grafana](/OPP-2023-lab-instruction.github.io/images/network.png)


Dans la vue Network Graph, vous pouvez configurer le type de connexions que vous souhaitez voir. Dans la section Flux (en haut à gauche), sélectionnez :

- Actif pour afficher uniquement les connexions actives.

- Autorisé à afficher uniquement les connexions réseau autorisées.

- Tout pour afficher les connexions réseau actives et autorisées.

## Enfreindre

Les violations enregistrent tous les moments spécifiques où un critère de stratégie a été rempli par l'un des objets de votre cluster : images et leurs composants, déploiements, activité d'exécution.

Considérez-le comme le « flux » d’événements qui se sont produits, même si nous ne voulons pas qu’il s’agisse simplement d’une liste de « choses à faire » pour les responsables de la réponse aux incidents.


![Grafana](/OPP-2023-lab-instruction.github.io/images/violations1.png)

Cliquez sur n'importe quelle violation, les détails de la violation apparaissent.


![Grafana](/OPP-2023-lab-instruction.github.io/images/violation2.png)


## Opérateur de conformité

Compliance Operator permet aux administrateurs d'OpenShift Container Platform de définir l'état de conformité souhaité d'un cluster et fournit un aperçu des lacunes et des moyens de remédier à toute stratégie non conforme.
L'opérateur de conformité évalue à la fois les ressources de l'API Kubernetes et les ressources d'OpenShift Container Platform, ainsi que les nœuds exécutant le cluster. L'opérateur de conformité utilise OpenSCAP, un outil certifié NIST, pour analyser et appliquer les politiques de sécurité fournies par le contenu.

Cliquez sur « Analyse de l'environnement »


![Grafana](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Gestion de la configuration

Avec Configuration Management, fournit une gestion de configuration efficace qui combine toutes ces entités distribuées sur une seule page. Il rassemble des informations sur tous vos clusters, espaces de noms, nœuds, déploiements, images, secrets, utilisateurs, groupes, comptes de service et rôles dans une seule vue de gestion de configuration, vous aidant à visualiser différentes entités et les connexions entre elles.


## Gestion des politiques

Avec la gestion des politiques, RHACS vous permet d'utiliser des politiques de sécurité prêtes à l'emploi et de définir des politiques multifacteurs personnalisées pour votre environnement de conteneurs.
La configuration de ces stratégies vous permet d'empêcher automatiquement les déploiements de services à haut risque dans votre environnement et de répondre aux incidents de sécurité d'exécution.


![Grafana](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


Toutes les politiques fournies avec le produit sont conçues dans le but de fournir des mesures correctives ciblées qui améliorent le renforcement de la sécurité.

Vous verrez que cette liste contient de nombreuses politiques de temps de construction et de déploiement pour détecter les erreurs de configuration au début du pipeline, mais également des politiques d'exécution qui renvoient à des recommandations de renforcement spécifiques.

Ces politiques proviennent de Red Hat : notre expertise, notre interprétation des meilleures pratiques du secteur et notre interprétation des normes de conformité communes, mais vous pouvez les modifier ou créer les vôtres.

