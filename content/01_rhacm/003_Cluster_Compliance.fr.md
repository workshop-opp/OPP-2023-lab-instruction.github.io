---
title: "Cluster Compliance"
draft: false
weight: 4
---

## Contexte

Suite au déploiement de nos clusters OpenShift, il nous a été demandé de mettre en place des règles de gouvernance pour assurer la sécurité et la performance des environnements. Parmi ces règles, deux politiques spécifiques ont été définies : la politique de supervision "policy-checkclusteroperator" visant à garantir que tous les opérateurs de cluster sont au statut "ready", et la politique "policy-resourcequota-florian" ayant pour objectif de limiter à 10 le nombre de pods déployés dans le namespace "florian-namespace".

## Objectif de l'exercice

L'objectif principal de cet exercice est de créer la politique "policy-resourcequota-florian" pour restreindre le nombre de pods dans le namespace spécifié. Ensuite, nous devrons appliquer les 2 policy aux clusters "sno-dev" et "sno-prod" en utilisant des "policysets".

## Étapes de l'exercice

Accedez a la section gouvernance de RHACM puis sur Policies.  Cliquez alors sur Create-policy.

Selectionner le toggle pour avoir la vu Yaml active. Copier le yaml ci-dessous :

```shell
apiVersion: policy.open-cluster-management.io/v1
kind: Policy
metadata:
  name: policy-resourcequota-florian
  namespace: policy-management
  annotations:
    policy.open-cluster-management.io/categories: SC System and Communications Protection
    policy.open-cluster-management.io/controls: SC-6 Resource Availability
    policy.open-cluster-management.io/standards: NIST SP 800-53
spec:
  disabled: false
  policy-templates:
    - objectDefinition:
        apiVersion: policy.open-cluster-management.io/v1
        kind: ConfigurationPolicy
        metadata:
          name: policy-resourcequota-example
        spec:
          namespaceSelector:
            include:
              - default
          object-templates:
            - complianceType: musthave
              objectDefinition:
                apiVersion: v1
                kind: ResourceQuota
                metadata:
                  name: example-resource-quota
                spec:
                  hard:
                    pods: "10"
          remediationAction: inform
          severity: medium
  remediationAction: enforce
```

Cela auto-remplis le formulaire. Apres avoir compris le fonctionnement de la policy, cliquez sur Next puis Submit pour creer la Policy.




## A vous de jouer 

A partir de votre nouvelle policy et de la policy generique policy-checkclusteroperator. Creez un nouveau policySet qui permettre d'appliquer vos Policy au cluster sno-prod et sno-dev. Vous utiliserez le namespace Policy-management lorsqu'un namespace vous sera demande.

## Solution