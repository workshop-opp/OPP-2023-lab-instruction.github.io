+++
title = "RHACM (1h)"
weight = 2
chapter = true
pre = "<b>2. </b>"
+++

# RHACM

## Summary

## Cluster Creation (make by the instructor)

In prerequisites to this course, aws credentials have been created from access key and secret key.

- From the navigation menu, navigate to Automate infrastructure > Clusters.


- On the Clusters page, Click Create Cluster. And Select Amazon Web Services. Select Standalone.

![RHACM Infrastructure](/OPP-2023-lab-instruction.github.io/images/rhacm-infrastructure.png)

- We will now complete the form to Create Cluster with the below details 

| Parameters | Value |
|----------|----------|
| Infrastructure provider credential | aws-credentials |
| Cluster name | sno-demo |
| Cluster set | default |
| Base DNS domain | sandbox2156.opentlc.com |
| Release image | OpenShift 4.14.3 |
| Parameters | Value |
|----------|----------|
| Region | eu-west-2 |

Then we will modify directly the yaml file to create an SNO instead of a full Openshift Cluster.

To make that switch the toggle to get `Yaml: On` and click on install-config folder.

![Yaml On](/OPP-2023-lab-instruction.github.io/images/yaml-on.png)

Then Update master replicas from 3 to 1 and worker replicas from 3 to 0.

You should now have the below install config.yaml.

- Now click Next, until the review, and Finally Click on Create.

- You can now follow the process of the cluster Creation in the RHACM UI with Cluster Install logs. 

![[Installation Process]](/OPP-2023-lab-instruction.github.io/images/creating-cluster-sno-demo.png)

- At the end you should see Your newly create cluster in the Ready States in the UI.

