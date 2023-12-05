---
title: "Observability"
draft: false
weight: 2
---


## Contexte :

In our production cluster environment, we recently encountered a critical issue related to over-allocation of resources by one of the teams. This led to CPU request engagement exceeding 300%. This situation compromises the availability and stability of our infrastructure, requiring rapid identification of overloaded namespace and implementation of quota control measures to prevent future incidents.

## Goal :

The objective of this exercise is to detect the namespace and deployment responsible for the excessive cpu request allocation and to patch it.

## Actions :

Access the production cluster and collect information about resource usage.

To do this, go to the Infrastructure section and click on Grafana (top left).

![Grafana](/OPP-2023-lab-instruction.github.io/images/grafana-access.png)

A certain number of dashboards are present by default when installing observability. To access it, click on Dashboards then Browse.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/browse-dashboard.png)

## Your turn 

From these different dashboards we ask you to find which deployment has the CPU request overestimated by mistake (100 cpu instead of 100 milli-cpu). When you have found the name of the namesapce, apply the following patch to it to remedy the overallocation:

```shell
oc patch deployment <deployment-name> -p '{"spec":{"template":{"spec":{"containers":[{"name":"<deployment-name>","resources":{"requests":{"cpu":"10m"}}}]}}}}' -n <namespace-name>
```

## Solution

{{%expand "Solution" %}}

The CPU quota table is available in the Dashboard General/Kubernetes/Compute Resources/Cluster. Once in this dashboard select the sno-prod Cluster. In the Cpu Quota Table click on CPU Requests to sort them in order. You should then observe that the Mirage namespace has a request of 100 cpu while it only uses 0.001. So this is the problematic namesapce.


![Dashboard](/OPP-2023-lab-instruction.github.io/images/tableau-cpu.png)

Connect to the sno-prod cluster and go to the mirage namespace. Click Workloads > Pods. We observe that the todo-app pods are in Pending status because the nodes do not have enough resources to respond to our request. We observe that the Deployment associated with it is todo-app. So all we have to do is apply the next patch.

![Request](/OPP-2023-lab-instruction.github.io/images/resource-request.png)

```shell
oc patch deployment todo-app -p '{"spec":{"template":{"spec":{"containers":[{"name":"todo-app","resources":{"requests":{"cpu":"10m"}}}]}}}}' -n mirage
```

{{% /expand%}}











