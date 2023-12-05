---
title: "Interface Walkthrough"
draft: false
weight: 1
---

On the following activity, we'll take a quick look at the main features of Red Hat Advanced Cluster Security.


## Vulnerability Management

Vulnerability management provides a dashboard containing important information about the applications deployed on the cluster. It mainly shows which vulnerabilities (including CVEs) are the most widespread or the most recent, and where the Docker images used originate. The dashboard also shows which vulnerabilities are present in the cluster.


![Vulnerabilités](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

Protect your containers against vulnerabilities from the moment images are created through to deployment and execution. RHACS can block the deployment of vulnerable images and integrates with your approved registries, including OpenShift Container Registry, for granular policy enforcement. RHACS also provides extensive support for third-party scanners such as Anchore, Red Hat Quay, Clair and Tenable to complement your existing image scanning tools.

## Risk Management


Let's take a look at the Risk view, where we go beyond the basics of vulnerabilities to understand how deployment configuration and execution activity affect the likelihood of an exploit occurring, and how successful these exploits will be.


![Riks](/OPP-2023-lab-instruction.github.io/images/risk.png)


This list displays all deployments, in all clusters and namespaces, sorted by risk priority.
Risk is calculated according to application activity, number of deployments and CVEs present.
The view is prioritized.
This feature enables you to concentrate your efforts on the deployments that present the greatest risk.



## Network Graph

The Network Graph is a flow diagram, firewall diagram and firewall rule generator in one.


![Network](/OPP-2023-lab-instruction.github.io/images/network.png)


Network Graph is a function for visualizing deployments in your namespaces.
It shows you, in the form of a flow diagram, the various connections existing on your different pods.
Based on the diagram, you can make decisions about adding or removing flows.
The best thing about Network Graph is that RHACS can generate network policies to protect and partition your connection flows.


## Violation

Violations is a feature in the form of a log that records all the specific moments when a CVE or policy created by the security team has been discovered by one of the objects in your cluster: images and their components, deployments, runtime.

This registry enables you to see at a glance the vulnerabilities present in your applications, specifying information such as :
- the namespace concerned
- type: specifies whether the vulnerability or policy is present in a deployment, secret, namespace, etc.
- enforced: whether or not the deployment has been blocked
- severity level
- vulnerability category
- when the vulnerability or policy was detected (build,deployment,runtime)
  

![Violations](/OPP-2023-lab-instruction.github.io/images/violations1.png)

Click on any violation to see more details.


![Violations2](/OPP-2023-lab-instruction.github.io/images/violation2.png)


## Compliance Operator

Compliance Operator provides you with a dashboard that lets you access defined metrics to see the state of compliance required in certain fields of activity, such as banking and medical.
Complance Operator evaluates both Kubernetes API resources and Openshift resources, as well as the nodes running the cluster.
This feature uses OpenSCAP, a NIST-certified tool, to analyze and apply the security policies provided by the content.


Click on "Scan Environnement"


![Compliance_Operator](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Configuration Management

Configuration Management, provides efficient configuration management that combines all entities on a single page. It gathers information on all your clusters, namespaces, nodes, deployments, images, secrets, users, groups, service accounts and roles in a single view, helping you to visualize different entities and the connections between them.


## Policy Management

With policy management, RHACS lets you use ready-to-use security policies and define customized multi-factor policies for your container environment.
By configuring these policies, you can automatically prevent the deployment of high-risk services in your environment and respond to runtime security incidents.

![Policy](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


All the policies supplied with the product are designed with the aim of providing targeted corrective measures that enhance security hardening.

You'll see that this list contains many build-time and deployment policies to detect configuration errors early in the pipeline, but also run-time policies that refer to specific hardening recommendations.



