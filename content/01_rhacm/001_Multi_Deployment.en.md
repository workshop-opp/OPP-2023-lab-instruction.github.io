---
title: "Application Deployment and  Management"
draft: false
weight: 2
---



## Goal:
Deploy an application using Red Hat ACM application deployment.

___
## Actions:
In this section, you will deploy the `airports-frontend` application.

`airports-frontend` a simple map frontend which display some airports on a world map.

Application source code is available on : https://github.com/workshop-opp/airports-frontend


___
__1. Deploy an application using ACM one 1 managed cluster__

Using Red Hat ACM, deploy the `airports-frontend` on the **sno-dev** cluster :

- The name of _your_ application must be **"\<youruser>-airpoirts-frontend"**.
- It must be deployed in the namespace **"\<youruser>-airpoirts-frontend"**.
- All kubernetes manifests are available in the **k8s** subdirectory in the [github repository](https://github.com/workshop-opp/airports-frontend)
- Use the good Label to deploy only on the dev cluster for now
- Verify the deployment in the ACM Topology view
- Access the airport application using its route


{{%expand "Guided Solution ? Click here" %}} 
Solution 
{{% /expand%}}

___
__2. Deploy the application on all cluster__

Modify your ACM application **"\<youruser>-airpoirts-frontend"** to deploy it on both **sno-dev** and **sno-prod** clusters.
- Edit your application
- Create a new Placement rule to allow deployment on both clusters (tips : check common label on both clusters before)


{{%expand "Guided Solution ? Click here" %}} 
Solution 
{{% /expand%}}