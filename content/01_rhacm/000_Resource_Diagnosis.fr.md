---
title: “Observability”
draft: false
weight: 1
---


## Context :

In our production cluster environment, we recently encountered a critical issue related to over-allocation of resources by one of the teams. This led to over 300% CPU request engagement. This situation compromises the availability and stability of our infrastructure, requiring rapid identification of overloaded namespaces and implementation of quota control measures to prevent future incidents.

## Objective of the exercise:

The goal of this exercise is to detect the namespace and deployment responsible for the CPU request overallocation and fix it.

## Exercise steps:

Access the production cluster and collect information about resource usage.

To do this, go to the Infrastructure section and click on Grafana (top left).

![Grafana](/OPP-2023-lab-instruction.github.io/images/grafana-access.png)

A number of dashboards are present by default when installing observability. To access it, click on Dashboards then Browse.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/browse-dashboard.png)

## Up to you

From these different dashboards, we ask you to find which deployment has the CPU demand overestimated by mistake (100 cpu instead of 100 milli-cpu). When you find the nameapce, apply the following patch to it to address overuse:

```shell
Patch deployment oc <deployment-name> -p '{"spec":{"template":{"spec":{"containers":[{"name":"<deployment-name>","resources": { "requests":{"cpu":"10m"}}}]}}}}' -n <namespace name>
```

## Solution

{{%expand "Solution" %}}

The CPU quota table is available in the General/Kubernetes/Compute Resources/Cluster dashboard. Once in this dashboard, select the sno-prod cluster. In the CPU quota table, click CPU Requests to sort them in order. You should then observe that the Mirage namespace has a request of 100 cpu while it only uses 0.001. So that's the namespace problem.

{{% /develop%}}