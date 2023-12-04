---
title: "Architecture"
draft: false
weight: 2
---

## Architecture

![lab Architecture](/OPP-2023-lab-instruction.github.io/images/lab-architecture.png)



The lab architecture will leverage two distinct OpenShift clusters to facilitate an immersive learning experience. Firstly, a designated Hub cluster will serve as the foundation for hosting the Red Hat Advanced Cluster Management (RHACM) and Red Hat Advanced Cluster Security (RHACS) tools. This cluster will act as the centralized control and management hub.

The second cluster, termed the Managed cluster, will be utilized as the focal point for implementing our multi-cluster management rules and security policies. Here, participants will witness practical application scenarios, observing firsthand how these policies are enforced and managed across the interconnected clusters.

This setup allows for a comprehensive understanding of the relationship between the Hub cluster, responsible for deploying and managing the RHACM and RHACS tools, and the Managed cluster, where these tools' functionalities will be practically applied to showcase effective multi-cluster management and stringent security policy enforcement.

## Red Hat Products

* The multi-cluster management capabilities are powered by ***Red Hat Advanced Cluster Management (RHACM)***, offering comprehensive control and oversight across interconnected clusters.

* For stringent and proactive security measures, we rely on ***Red Hat Advanced Cluster Security (RHACS)***, ensuring robust protection and policy enforcement.

* Additionally, the container image repository is supported by ***Red Hat Quay***, offering secure storage and distribution of container images.
* 
While this lab is currently hosted on the Red Hat Product Demo System (RHPDS) due to logistical and cost considerations, there are possibilities for future deployments:

* The primary hub infrastructure could potentially leverage a Managed Services offering of OpenShift, such as Red Hat OpenShift on AWS (ROSA) or Azure Red Hat OpenShift (ARO), offering scalable and managed solutions.

* For other cluster requirements, options like Single Node OpenShift or a Compact Cluster can be explored, providing flexibility and scalability based on specific needs and resource constraints.