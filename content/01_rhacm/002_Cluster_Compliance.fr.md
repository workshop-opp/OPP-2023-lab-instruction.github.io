---
title: "Conformité Cluster"
draft: false
weight: 2
---

## Contexte

Suite au déploiement de nos clusters OpenShift, il nous a été demandé de mettre en place des règles de gouvernance pour assurer le bon fonctionnement des environnements. Parmi ces règles, deux politiques spécifiques ont été définies : la politique de supervision **policy-checkclusteroperator** visant à garantir que tous les opérateurs de clusters sont en statut "ready", et la politique **policy-resourcequota-<VOTRE_VILLE>** visant à limiter le nombre de pods déployé dans le namespace **<VOTRE_VILLE>-ns** à 10.

## Objectif de l'exercice

L'objectif de cet exercice est de créer la politique **policy-resourcequota-<VOTRE_VILLE>** pour restreindre le nombre de pods dans le namespace spécifié. Ensuite, nous devrons appliquer les 2 politiques (resourcequota and checkclusteroperator) aux clusters « sno-dev » et « sno-prod » en utilisant un « Policysets ».

{{% notice note %}}
La Policy **policy-checkclusteroperator** existe déjà et n’a donc pas besoin d’être recréée.
{{% /notice %}}


## Étapes de l'exercice

Accédez à la section gouvernance de RHACM puis cliquez sur Policies. Cliquez ensuite sur Créer une politique.

![Governance](/OPP-2023-lab-instruction.github.io/images/governance.png)

Sélectionnez le toggle pour activer la vue Yaml. Copiez le yaml ci-dessous :

{{% notice info %}}
N'oubliez pas de mettre à jour **<VOTRE_VILLE>** dans le manifeste ci-dessous avant de l'appliquer.
{{% /notice %}}


```shell
apiVersion: policy.open-cluster-management.io/v1
kind: Policy
metadata:
  name: policy-resourcequota-<VOTRE_VILLE>
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
          name: policy-resourcequota-<VOTRE_VILLE>
        spec:
          namespaceSelector:
            include:
              - <VOTRE_VILLE>-ns
          object-templates:
            - complianceType: musthave
              objectDefinition:
                apiVersion: v1
                kind: ResourceQuota
                metadata:
                  name: example-resource-quota
                spec:
                  hard:
                    pods: "2"
          remediationAction: inform
          severity: medium
  remediationAction: enforce
```

Cela remplit automatiquement le formulaire. Après avoir compris le fonctionnement de la stratégie, cliquez sur Suivant puis sur Soumettre pour créer la stratégie.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy-yaml.png)



## A vous de jouer 

À partir de votre nouvelle policy et de la policy policy-checkclusteroperator, créez un nouveau PolicySet **policyset-<VOTRE_VILLE>** qui vous permettra d'appliquer vos politiques au cluster sno-prod et sno-dev. 

{{% notice tip %}}
Vous utiliserez le namespace de policy-management lorsqu’on vous demandera un namespace.
{{% /notice %}}


## Solution

{{%expand "Solution guidée" %}}

Allez dans la section PolicySet et cliquez sur Créer un policySet. Mettez **policyset-<VOTRE_VILLE>** comme nom et policy-management comme namespace.

Check  Policy-checkclusteroperator et votre Policy nouvellement créée.

![Policy](/OPP-2023-lab-instruction.github.io/images/create-policyset.png)

Dans la partie placement Section, select `dev` and `prod`.

![Policy](/OPP-2023-lab-instruction.github.io/images/placement.png)

Cliquez sur Submit.

Vous pourrez alors observer le policy report de votre policyset.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy-report.png)

{{% notice tip %}}
Pour valider, vous pouvez essayer de scale un déploiement jusqu'à 12 dans le namesapce **<VOTRE_VILLE>-ns** de l'un des clusters gérés pour vérifier l'effet des resourcesQuotas.
{{% /notice %}}

{{% /expand%}}