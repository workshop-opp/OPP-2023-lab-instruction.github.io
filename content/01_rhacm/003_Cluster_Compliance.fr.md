---
title: "Cluster Compliance"
draft: false
weight: 4
---

## Contexte

Suite au déploiement de nos clusters OpenShift, il nous a été demandé de mettre en place des règles de gouvernance pour assurer la sécurité et la performance des environnements. Parmi ces règles, deux politiques spécifiques ont été définies : la politique de supervision "policy-checkclusteroperator" visant à garantir que tous les opérateurs de clusters sont en statut "ready", et la politique "policy-resourcequota-florian" visant à limiter le nombre de pods. déployé dans l’espace de noms « florian-namespace » à 10.

## Objectif de l'exercice

L'objectif principal de cet exercice est de créer la politique « policy-resourcequota-florian » pour restreindre le nombre de pods dans l'espace de noms spécifié. Ensuite, nous devrons appliquer les 2 politiques aux clusters « sno-dev » et « sno-prod » en utilisant « Policysets ».

## Étapes de l'exercice

Accédez à la section gouvernance du RHACM puis sur Politiques. Cliquez ensuite sur Créer une politique.

Sélectionnez la bascule pour activer la vue Yaml. Copiez le yaml ci-dessous :

```coquille
Version api : policy.open-cluster-management.io/v1
genre : Politique
métadonnées :
    nom : politique-ressourcequota-florian
    espace de noms : gestion des politiques
    Remarques:
      Policy.open-cluster-management.io/categories : Protection du système SC et des communications
      Policy.open-cluster-management.io/controls : Disponibilité des ressources SC-6
      Policy.open-cluster-management.io/standards : NIST SP 800-53
spécification :
    désactivé : faux
    modèles de politique :
      - définition de l'objet :
          Version api : policy.open-cluster-management.io/v1
          genre : Politique de configuration
          métadonnées :
            nom : politique-ressourcequota-exemple
          spécification :
            sélecteur d'espace de noms :
              inclure:
                -défaut
            modèles d'objet :
              - ComplianceType : musthave
                définition de l'objet :
                  Version de l'API : v1
                  genre : Quota de ressources
                  métadonnées :
                    nom : exemple-ressource-quota
                  spécification :
                    dur:
                      dosettes : "10"
            remédiationAction : informer
            gravité : moyenne
    remediationAction : appliquer
```

Cela remplit automatiquement le formulaire. Après avoir compris le fonctionnement de la stratégie, cliquez sur Suivant puis sur Soumettre pour créer la stratégie.




## À toi de voir

À partir de votre nouvelle stratégie et de l'opérateur générique Policy-checkclusteroperator. Créez un nouveau PolicySet qui vous permettra d'appliquer vos politiques au cluster sno-prod et sno-dev. Vous utiliserez l’espace de noms de gestion des stratégies lorsqu’on vous demandera un espace de noms.

## Solution