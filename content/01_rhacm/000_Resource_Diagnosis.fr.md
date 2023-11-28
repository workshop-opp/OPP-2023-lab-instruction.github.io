---
title: "Resource Diagnosis"
draft: false
weight: 1
---

## Goal:
Résolvez l’échec du déploiement causé par les limitations de quotas et déployez avec succès l’application en ajustant les quotas OpenShift.

## Actions:
Essayez de déployer l'application dans OpenShift.

Utiliser
```coquille
oc new-app <application_manifest> pour lancer le déploiement.
```
Cliquez sur le bouton "Déployer" dans la console OpenShift.
Identifiez les contraintes de ressources dans Grafana de RHACM.

Accédez au tableau de bord Grafana de RHACM.
Sélectionnez le cluster, accédez à « Observabilité » > « Grafana ».
Observez les mesures d’utilisation des ressources.
Confirmez les problèmes de quota affectant le déploiement.

Examinez les métriques Grafana indiquant les contraintes de ressources.
Ajustez les quotas dans OpenShift.

Localisez « Quotas de ressources » dans la console OpenShift.
Modifiez le quota spécifique impacté par le problème de déploiement.
Augmentez les limites de ressources si nécessaire.
Redéployez l'application.

Utiliser
```
dernier déploiement d'oc <application_deployment>
```
pour le redéploiement.
Surveillez l’état du déploiement pour assurer sa réussite.