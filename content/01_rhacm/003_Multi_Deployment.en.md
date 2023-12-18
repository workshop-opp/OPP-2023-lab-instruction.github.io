---
title: "Deployment and management of an application"
draft: false
weight: 3
---


## Context

Our application **airports-frontend** is a frontend written in [quarkus](https://quarkus.io) and displaying airports as well as planes moving between airports. However, on this workshop, we will only deal with the frontend and we will not see the planes moving.

Our application being more and more critical, it was decided to deploy it on 2 different clusters.


## Objective of the exercise

The objective of this exercise is to deploy our **airports-frontend** application in multi-cluster mode using the OpenShit Advanced Cluster Managment mechanisms.

## Exercise steps

From the OpenShift Hub cluster, access the ACM interface.
To do this, at the top of the screen, click on **local-cluster** then **All Clusters**:

![ACM Console](/OPP-2023-lab-instruction.github.io/images/acm-startconsole.png)


Then go to the **Applications** section

![ACM Applications](/OPP-2023-lab-instruction.github.io/images/acm-applications.png)


## Up to you

1 - __Deployment on the development cluster__
- Create a **Subscription** type application (**Application Set** type would need the installation of argoCD which is not what we want here)
- Its name will be **<YOUR_CITY>-airports-frontend**
- Its namespace will be **<YOUR_CITY>-ns**
- Repository **Git** based on [airports-frontend](https://github.com/workshop-opp/airports-frontend.git)
- Branch: **main**
- Path: **k8s**
- Deploy the application on the Cluster sets **global** and choose 1 label identifying ONLY our development cluster

{{% notice tip %}}
Tip: you can find all the labels for each cluster in the Infrastructure menu
{{% /notice %}}

- Check in the **Topology** tab that the application has been deployed on the right cluster (you can also connect to the OpenShift console of the Dev cluster and check that the new namespace contains your application)

## Solution

{{%expand "Guided solution" %}}

Complete the form as shown below (replacing `tokyo` with the name of your city).

![ACM Applications step 1](/OPP-2023-lab-instruction.github.io/images/create-application-step-1.png)

In the Infrastructure tab, you probably noticed that an `environment=dev` label has been applied to the development cluster. This is the one we are going to use.

![ACM Applications step 2](/OPP-2023-lab-instruction.github.io/images/create-application-step-2.png)

Then click Create at the top right.

You should observe that your application deployment works well in the topology view.

![Topology part 1 ](/OPP-2023-lab-instruction.github.io/images/topology-part1.png)

By clicking on route then `launch route url` you should see the application below.

![Airport application sno dev](/OPP-2023-lab-instruction.github.io/images/airport-application-sno-dev.png)

{{% notice note %}}
You will notice in the URL that the application was deployed to sno-dev as expected.
{{% /notice %}}


{{% /expand%}}


2 - __Deployment on the Dev and Prod cluster simultaneously__

- Return to your application **<YOUR_CITY>-airports-frontend**
- Edit there
- Create a new placement rule using a label **common** to the 2 clusters
- Observe and verify that your application is deployed on the 2 clusters

## Solution

{{%expand "Guided solution" %}}

In the application section, find your previously created application and then click on it.

![Search application](/OPP-2023-lab-instruction.github.io/images/application-search.png)

Click Actions > Edit Application at the top right. Then open the Select clusters for application deployment section and click `Deploy application resources on clusters with all specified labels`. In ClusterSet use global again and in label select deploy=acm.



![deploy dev and prod](/OPP-2023-lab-instruction.github.io/images/deploy-dev-and-prod.png)

In the topology view, you should now see that the application has been deployed to the development and production clusters.

![Topology part 2](/OPP-2023-lab-instruction.github.io/images/topology-part2.png)



{{% /expand%}}


3 - __BONUS exercise: GitOps with ACM__

We will observe the GitOps mechanisms offered by ACM: to do this, you will **REQUIRED** have a GitHub account.
- Connect with your personal login to [GitHub](https://github.com)
- Fork the repository https://github.com/workshop-opp/airports-frontend
- Modify the **<YOUR_USER>-airports-frontend** application to use the repository you just forked (https://github.com/<YOUR_USER_GITHUB/airports-frontend)
- Change the number of replicas in the `k8s/deployment.yaml` file in YOUR account's repository
- Observe the change in the number of PODs deployed

{{%expand "Guided solution" %}}

TODO

{{% /expand%}}