---
title: "Cluster Compliance"
draft: false
weight: 2
---

## Context

Following the deployment of our OpenShift clusters, we were asked to implement governance rules to ensure the security and performance of the environments. Among these rules, two specific policies have been defined: the "policy-checkclusteroperator" supervision policy aimed at ensuring that all cluster operators are in "ready" status, and the "policy-resourcequota-<YOUR_COUNTRY>" policy aimed at limiting the number of pods. deployed in the “<YOURCOUNTRY>-ns” namespace at 10.

## Objective of the exercise

The main goal of this exercise is to create the policy “policy-resourcequota-<YOURCOUNTRY>” to restrict the number of pods in the specified namespace. Next, we will need to apply the 2 policies (resourcequota and checkclusteroperator) to the “sno-dev” and “sno-prod” clusters using “Policysets”.

## Exercise steps

Go to the RHACM governance section then on Policies. Then click Create Policy.

![Governance](/OPP-2023-lab-instruction.github.io/images/governance.png)

Select the toggle to enable Yaml view. Copy the yaml below:

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

This automatically fills out the form. After you understand how the policy works, click Next and then Submit to create the policy.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy-yaml.png)




## Up to you

From your new policy and the generic Policy-checkclusteroperator operator. Create a new PolicySet policyset-<YOURCOUNTRY> that will allow you to apply your policies to the sno-prod and sno-dev cluster. You will use the policy-management namespace when asked for a namespace.

## Solution

{{%expand "Guided solution" %}}

Go In Policy sets section and click on Create Policy set. Put policyset-<YOURCOUNTRY> as Name and policy-management as Namespace.

Check the policy-checkclusteroperator and your newly created policy.

![Policy](/OPP-2023-lab-instruction.github.io/images/create-policyset.png)

In the placement Section, select `dev` and `prod`.

![Policy](/OPP-2023-lab-instruction.github.io/images/placement.png)

Finally click on Submit.

To validate you can try to scale a deployment up to 10 in one of the managed cluster to check the effect of resourcesQuotas.

{{% /expand%}}
