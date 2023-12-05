---
title: "Application Deployment and Management"
draft: false
weight: 3
---

## Context

Our application **airports-frontend** is a frontend written in [quarkus](https://quarkus.io) and displaying airports as well as planes moving between airports. However, within the framework of this workshop, we will only deal with the frontend here and we will not see the planes moving.

Our application being more and more critical, it was decided to deploy it on 2 different clusters.


## Goal

The objective of this exercise is to deploy our **airports-frontend** application in multi-cluster mode using the OpenShit Advanced Cluster Managment mechanisms.

## Actions

From the OpenShift Hub cluster, access the ACM interface.
To do this, at the top of the screen, click on **local-cluster** then **All Clusters**:

![ACM Console](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)


Then go to the **Applications** section

![ACM Applications](/OPP-2023-lab-instruction.github.io/images/acm-applications.png)


## Your turn 

1 - __Deployment on the development cluster__
- Create a **Subscription** type application
- Its name will be **<YOUR_USER>-airports-frontend**
- Its namespace will be **<YOUR_USER>-airports-frontend**
- Repository **Git** based on [airports-frontend](https://github.com/workshop-opp/airports-frontend.git)
- Branch: **main**
- Path: **k8s**
- Deploy the application on the Cluster sets **default** and choose 1 label identifying ONLY our development cluster (tip: you can find all the labels for each cluster in the Infrastructure menu)
- Check in the **Topology** tab that the application has been deployed on the right cluster (you can also connect to the OpenShift console of the Dev cluster and check that the new namespace contains your application)

## Solution

{{%expand "Solution" %}}


{{% /expand%}}


2 - __Deployment on the Dev and Prod cluster simultaneously__
- Return to your application **<YOUR_USER>-airports-frontend**
- Edit there
- Create a new placement rule using a common label to the 2 clusters
- Observe and verify that your application is deployed on the 2 clusters

## Solution

{{%expand "Solution" %}}


{{% /expand%}}


3 - __BONUS exercise: GitOps with ACM__

We will observe the GitOps mechanisms offered by ACM: to do this, you will **REQUIRED** have a GitHub account.
- Connect with your personal login to [GitHub](https://github.com)
- Fork the repository https://github.com/workshop-opp/airports-frontend
- Modify the **<YOUR_USER>-airports-frontend** application to use the repository you just forked (https://github.com/<YOUR_USER_GITHUB/airports-frontend)
- Change the number of replicas in the `k8s/deployment.yaml` file in YOUR account's repository
- Observe the change in the number of PODs deployed

{{%expand "Solution" %}}


{{% /expand%}}