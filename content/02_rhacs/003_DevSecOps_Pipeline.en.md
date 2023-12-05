---
title: "DevSecOps Pipeline"
draft: false
weight: 4
---

In this part, we will see how RHACS can be fully integrated into a DevSecOps approach.

For this, we have a pipeline available which aims to deploy an application on our cluster.

The goal of this pipeline is simply to git clone a repository, build the image and deploy it.
Between the build and deployment stage, we have 2 parallel stages: image-scan, image-check.
This is where RHACS comes in.

Thus, if RHACS detects a CVE present on the application image, the deployment will be blocked.


Let's move on to practice:

- Click on “START”
- Track pipeline progress steps

![Pipeline](/OPP-2023-lab-instruction.github.io/images/pipeline_1.png)



As you can see, the image-check step is blocked, because RHACS detected a violation which orders it to enforce the deployment.
This is why the pipeline has stopped and the application is not deployed.


Let's go to the RHACS dashboard and more precisely to the Violations section.


![Violations](/OPP-2023-lab-instruction.github.io/images/pipeline_2.png)

In the 1st line, you can see the policy pillow_policy which blocked the deployment of our application.
You can click on the policy for more details.
In our case, the policy blocked the deployment because in the application that we wish to deploy, there is indeed a CVE.
This CVE concerns pillow, a python library that allows you to manipulate images.
This CVE only exists on version 9.5.0 of pilow, but it is no longer present on the most recent version.

In another context, the developer will have to update his library, carry out unit and integration tests to check if this update does not infect the behavior of the application.

Then, he will have to restart the pipeline to deploy the new version of the application.

In our case, to explore the functionalities of RHACS, we will act directly on our RHACS dashboard.

To do this, we will indicate that we no longer wish to block the deployment of our application because of our CVE.
RHACS will simply inform us that a CVE is present on our application, nothing more.

Follow the steps:

- Click on Platform Configuration
- Policy Management
- Click on the “Filter policies” search bar, select “Policy”
- Type "pillow_policy", this is the policy which orders the blocking of the deployment of our application.
- Click on the policy
- at the top left, click on Actions, then edit policy.
- Go directly to section 2: Policy Behavior

![policy](/OPP-2023-lab-instruction.github.io/images/pipeline_3.png)

In the "Response method" section as above, "inform and enforce" is checked.

- Check “inform”
- Click Next until you are asked to save the policy.
- Save changes


Now go back to your pipeline and run again.

As you can see, the application is deployed on the cluster, without RHACS blocking the deployment.
However, if you return to the dashboard, RHACS only informs you again that a CVE is present in your application.