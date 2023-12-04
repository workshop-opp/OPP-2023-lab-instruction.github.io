---
title: "Architecture"
draft: false
weight: 2
---

## Architecture

![lab Architecture](/OPP-2023-lab-instruction.github.io/images/lab-architecture.png)


L'architecture du laboratoire exploitera deux clusters OpenShift distincts pour faciliter une expérience d'apprentissage immersive. Premièrement, un cluster Hub désigné servira de base pour l'hébergement des outils Red Hat Advanced Cluster Management (RHACM) et Red Hat Advanced Cluster Security (RHACS). Ce cluster fera office de centre de contrôle et de gestion centralisé.

Le deuxième cluster, appelé cluster géré, sera utilisé comme point focal pour la mise en œuvre de nos règles de gestion multicluster et de nos politiques de sécurité. Ici, les participants assisteront à des scénarios d'application pratiques, observant de première main comment ces politiques sont appliquées et gérées dans les clusters interconnectés.

Cette configuration permet une compréhension complète de la relation entre le cluster Hub, responsable du déploiement et de la gestion des outils RHACM et RHACS, et le cluster géré, où les fonctionnalités de ces outils seront appliquées pratiquement pour présenter une gestion multi-cluster efficace et une sécurité stricte. l'application de la politique.

## Produits Red Hat

* Les capacités de gestion multicluster sont optimisées par ***Red Hat Advanced Cluster Management (RHACM)***, offrant un contrôle et une surveillance complets sur les clusters interconnectés.

* Pour des mesures de sécurité strictes et proactives, nous nous appuyons sur ***Red Hat Advanced Cluster Security (RHACS)***, garantissant une protection et une application des politiques robustes.

* De plus, le référentiel d'images de conteneurs est pris en charge par ***Red Hat Quay***, offrant un stockage et une distribution sécurisés des images de conteneurs.
*
Bien que cet atelier soit actuellement hébergé sur le système de démonstration de produits Red Hat (RHPDS) pour des raisons de logistique et de coût, il existe des possibilités de déploiements futurs :

* L'infrastructure du hub principal pourrait potentiellement exploiter une offre de services gérés d'OpenShift, telle que Red Hat OpenShift sur AWS (ROSA) ou Azure Red Hat OpenShift (ARO), offrant des solutions évolutives et gérées.

* Pour d'autres exigences de cluster, des options telles que Single Node OpenShift ou Compact Cluster peuvent être explorées, offrant flexibilité et évolutivité en fonction des besoins spécifiques et des contraintes de ressources.