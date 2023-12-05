---
title: "Architecture"
draft: false
weight: 2
---

## Architecture

![lab Architecture](/OPP-2023-lab-instruction.github.io/images/lab-architecture.png)


L'architecture de ce workshop exploitera trois clusters OpenShift distincts pour faciliter une expérience d'apprentissage immersive. Premièrement, un cluster Hub servira de base pour l'hébergement des outils Red Hat Advanced Cluster Management (RHACM) et Red Hat Advanced Cluster Security (RHACS). Ce cluster fera office de centre de contrôle et de gestion centralisé.

Les deux autres cluster (sno-dev et sno-prod), appelés clusters gérés, seront utilisés pour la mise en œuvre de nos règles de gestion multicluster et de nos politiques de sécurité.

Cette configuration permet une compréhension complète de la relation entre le cluster Hub, responsable du déploiement et de la gestion des outils RHACM et RHACS, et les clusters gérés, où les fonctionnalités de ces outils seront appliquées pratiquement pour présenter une gestion multi-cluster efficace et une sécurité stricte.

## Produits Red Hat

* Les capacités de gestion multicluster sont optimisées par ***Red Hat Advanced Cluster Management (RHACM)***, offrant un contrôle et une surveillance completes sur les clusters managés.

* Pour la gestion de la sécurité sur nos clusters, nous nous appuyons sur ***Red Hat Advanced Cluster Security (RHACS)***, garantissant une protection et une application des politiques robustes.


Bien que cet atelier soit actuellement hébergé sur le système de démonstration de produits Red Hat (RHPDS) pour des raisons de logistique et de coût, il existe des possibilités de déploiements futurs :

* L'infrastructure du hub principal pourrait potentiellement exploiter une offre de services gérés d'OpenShift, telle que Red Hat OpenShift sur AWS (ROSA) ou Azure Red Hat OpenShift (ARO), offrant des solutions évolutives et managées.

