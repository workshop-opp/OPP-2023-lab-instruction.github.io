---
title: "Cluster Compliance"
draft: false
weight: 4
---

## Contexte

Suite au déploiement de nos clusters OpenShift, il nous a été demandé de mettre en place des règles de gouvernance pour assurer la sécurité et la performance des environnements. Parmi ces règles, deux politiques spécifiques ont été définies : la politique de supervision "policy-checkclusteroperator" visant à garantir que tous les opérateurs de clusters sont en statut "ready", et la politique "policy-resourcequota-<YOURCOUNTRY>" visant à limiter le nombre de pods. déployé dans le namespace « <YOURCOUNTRY>-ns » à 10.

## Objectif de l'exercice

L'objectif principal de cet exercice est de créer la politique « policy-resourcequota-<YOURCOUNTRY> » pour restreindre le nombre de pods dans l'espace de noms spécifié. Ensuite, nous devrons appliquer les 2 politiques (resourcequota and checkclusteroperator) aux clusters « sno-dev » et « sno-prod » en utilisant « Policysets ».

## Étapes de l'exercice

Accédez à la section gouvernance du RHACM puis sur Politiques. Cliquez ensuite sur Créer une politique.

![Governance](/OPP-2023-lab-instruction.github.io/images/governance.png)

Sélectionnez le toggle pour activer la vue Yaml. Copiez le yaml ci-dessous :

```shell
apiVersion: policy.open-cluster-management.io/v1
kind: Policy
metadata:
  name: policy-resourcequota-<YOURCOUNTRY>
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

Cela remplit automatiquement le formulaire. Après avoir compris le fonctionnement de la stratégie, cliquez sur Suivant puis sur Soumettre pour créer la stratégie.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy-yaml.png)


## A vous de jouer 

À partir de votre nouvelle policy et de la policy générique policy-checkclusteroperator. Créez un nouveau PolicySet qui vous permettra d'appliquer vos politiques au cluster sno-prod et sno-dev. Vous utiliserez le namespace de gestion des stratégies lorsqu’on vous demandera un espace de noms.

## Solution

{{%expand "Guided solution" %}}

Go In Policy sets section and click on Create Policy set. Put policyset-<YOURCOUNTRY> as Name and policy-management as Namespace.

Check the policy-checkclusteroperator and your newly created policy.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy_management.png)

In the placement Section, select `dev` and `prod`.

![Policy](/OPP-2023-lab-instruction.github.io/images/placement.png)

Finally click on Submit.

To validate you can try to scale a deployment up to 10 in one of the managed cluster to check the effect of resourcesQuotas.

{{% /expand%}}