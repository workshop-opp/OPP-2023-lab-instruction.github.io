---
title: "Cluster Compliance"
draft: false
weight: 4
---

## Context

Following the deployment of our OpenShift clusters, we were asked to implement governance rules to ensure the proper functioning of the environments. Among these rules, two specific policies have been defined: the supervision policy **policy-checkclusteroperator** aimed at guaranteeing that all cluster operators are in "ready" status, and the policy **policy-resourcequota-<YOUR_CITY> ** aimed at limiting the number of pods deployed in the namespace **<YOUR_CITY>-ns** to 10.

## Objective of the exercise

The objective of this exercise is to create the policy **policy-resourcequota-<YOUR_CITY>** to restrict the number of pods in the specified namespace. Then, we will have to apply the 2 policies (resourcequota and checkclusteroperator) to the “sno-dev” and “sno-prod” clusters using a “Policysets”.

{{% notice note %}}
The Policy **policy-checkclusteroperator** already exists and therefore does not need to be recreated.
{{% /notice %}}


## Exercise steps

Access the governance section of RHACM then click on Policies. Then click Create Policy.

![Governance](/OPP-2023-lab-instruction.github.io/images/governance.png)

Select the toggle to activate the Yaml view. Copy the yaml below:

{{% notice info %}}
Don't forget to update **<YOUR_CITY>** in the manifest below before applying it.
{{% /notice %}}


```shell
apiVersion: policy.open-cluster-management.io/v1
kind: Policy
metadata:
   name: policy-resourcequota-<YOUR_CITY>
   namespace: policy-management
   notes:
     policy.open-cluster-management.io/categories: SC System and Communications Protection
     policy.open-cluster-management.io/controls: SC-6 Resource Availability
     policy.open-cluster-management.io/standards: NIST SP 800-53
spec:
   disabled: false
   policy-templates:
     - objectDefinition:
         apiVersion: policy.open-cluster-management.io/v1
         kind:ConfigurationPolicy
         metadata:
           name: policy-resourcequota-example
         spec:
           namespaceSelector:
             include:
               - <YOUR_CITY>-ns
           object-templates:
             - complianceType: musthave
               objectDefinition:
                 api Version: v1
                 kind:ResourceQuota
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

From your new policy and the policy policy-checkclusteroperator, create a new PolicySet **policyset-<YOUR_CITY>** which will allow you to apply your policies to the sno-prod and sno-dev cluster.

{{% notice tip %}}
You will use the policy-management namespace when asked for a namespace.
{{% /notice %}}


## Solution

{{%expand "Guided solution" %}}

Go to the PolicySet section and click Create policySet. Put **policyset-<YOUR_CITY>** as name and policy-management as namespace.

Check Policy-checkclusteroperator and your newly created Policy.

![Policy](/OPP-2023-lab-instruction.github.io/images/create-policyset.png)

In the Placement Section, select `dev` and `prod`.

![Policy](/OPP-2023-lab-instruction.github.io/images/placement.png)

Click Submit.

You will then be able to observe the policy report of your policyset.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy-report.png)

{{% notice tip %}}
To validate, you can try scaling a deployment up to 12 in the namesapce **<YOUR_CITY>-ns** of one of the managed clusters to check the effect of resourcesQuotas.
{{% /notice %}}




{{% /expand%}}