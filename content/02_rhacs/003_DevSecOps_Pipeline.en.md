---
title: "DevSecOps Pipeline"
draft: false
weight: 4
---

In this section, we'll look at how RHACS can be fully integrated into a DevSecOps approach.


## Context


The development team uses a pipeline to clone a remote repository, build the image and deploy the application on the cluster.  
Between the build and deployment stages, we have 2 parallel steps: image-scan, image-check.
These steps enable RHACS to scan the application for vulnerabilities.

## Activity goals

The aim is to find out which critical vulnerabilities are present in the pipeline.


## Activity stages

To achieve the activity objective, you must :
- launch the pipeline to enable application deployment
- find the CVE present in the application
- Modify the policy corresponding to the policy to block further deployment
- Restart the pipeline



## Up to you

## Solution

{{%expand "Solution: Exporter la liste des Deployment touche par la CVE `CVE-2022-32207` " %}}



In Openshift Pipelines :
- Click on "START
- Follow the pipeline's progress


![Pipeline](/OPP-2023-lab-instruction.github.io/images/pipeline_1.png)


As you can see, the deployment went off without a hitch.

To find the CVE corresponding to the deployment, go to the RHACS dashboard and, more specifically, to the Violations section.

![Violations](/OPP-2023-lab-instruction.github.io/images/pipeline_2.png)

On the 1st line, you can see the pillow_policy that has blocked the deployment of our application (according to your namespace name).
You can click on the policy for more details.
This CVE concerns pillow, a python library for manipulating images.
This CVE exists only on version 9.5.0 of pilow, but is no longer present on the most recent version.

To block new deployments :

Follow the steps below:

- Click on Platform Configuration
- Policy Management
- Click on the "Filter policies" search bar, and select "Policy".
- Type "pillow_policy", this is the policy that will block the deployment of our application.
- Click on the policy
- at top left, click on Actions, then edit policy.
- Go directly to section 2: Policy Behavior

![policy](/OPP-2023-lab-instruction.github.io/images/pipeline_3.png)

In the "Response method" section, as above, "inform" is checked.

- Check "inform and enforce".
- Click Next until you are prompted to save the policy.
- Save changes


Now go back to your pipeline and run it again.

As you can see, the application is not deployed on the cluster, as RHACS is blocking deployment.



{{% /expand%}}


