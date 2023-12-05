---
title: "Cluster Compliance"
draft: false
weight: 4
---

## Context

Following the deployment of our OpenShift clusters, we were asked to implement governance rules to ensure the security and performance of the environments. Among these rules, two specific policies have been defined: the "policy-checkclusteroperator" supervision policy aimed at ensuring that all cluster operators are in "ready" status, and the "policy-resourcequota-florian" policy aimed at limiting the number of pods. deployed in the “florian-namespace” namespace at 10.

## Objective of the exercise

The main goal of this exercise is to create the policy “policy-resourcequota-florian” to restrict the number of pods in the specified namespace. Next, we will need to apply the 2 policies to the “sno-dev” and “sno-prod” clusters using “Policysets”.

## Exercise steps

Go to the RHACM governance section then on Policies. Then click Create Policy.

Select the toggle to enable Yaml view. Copy the yaml below:

```shell
API version: policy.open-cluster-management.io/v1
genre: Politics
metadata:
     name: policy-resourcequota-florian
     namespace: policy management
     Remarks:
       Policy.open-cluster-management.io/categories: SC System and Communications Protection
       Policy.open-cluster-management.io/controls: SC-6 resource availability
       Policy.open-cluster-management.io/standards: NIST SP 800-53
specification :
     disabled: false
     policy models:
       - object definition:
           API version: policy.open-cluster-management.io/v1
           genre: Config policy
           metadata:
             name: policy-resourcequota-example
           specification :
             namespace selector:
               include:
                 -default
             object models:
               - ComplianceType: musthave
                 object definition:
                   API version: v1
                   gender: Resource quota
                   metadata:
                     name: example-resource-quota
                   specification :
                     hard:
                       pods: “10”
             remediationAction: inform
             severity: medium
     remediationAction: apply
```

This automatically fills out the form. After you understand how the policy works, click Next and then Submit to create the policy.




## Up to you

From your new policy and the generic Policy-checkclusteroperator operator. Create a new PolicySet that will allow you to apply your policies to the sno-prod and sno-dev cluster. You will use the policy management namespace when asked for a namespace.

## Solution