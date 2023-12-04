---
title: "Interface Walkthrough"
draft: false
weight: 1
---

Through the following pages, we will quickly see the functionalities available on Red Hat Advanced Cluster Security 


## Vulnerability Management

The overview provides several important reports - where the vulnerabilities are, which are the most widespread or the most recent, where my Docker images are coming from, and important vulnerabilities in OpenShift itself.


![Grafana](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

Protect your containers against vulnerabilities from the time images are built until they’re deployed and running. RHACS can block vulnerable images from being deployed and integrates with your approved registries, including OpenShift Container Registry, for granular policy enforcement. RHACS also provides extensive support for third-party scanners such as Anchore, Red Hat Quay, Clair, and Tenable to augment your existing image scanning tools.


## Risk Management


Let’s take a look at the Risk view, where we go beyond the basics of vulnerabilities to understand how deployment configuration and runtime activity impact the likelihood of an exploit occurring and how successful those exploits will be.


![Grafana](/OPP-2023-lab-instruction.github.io/images/risk.png)


This list view shows all deployments, in all clusters and namespaces, ordered by Risk priority.

Risk is also influenced by runtime activity - and Deployments that have activity that could indicate a breach in progress have a red dot on the left. Obviously - the first one in the list should be our first focus.

The reality of security is that it’s just not possible to tackle all sources of Risk, so organizations end up prioritizing their efforts. We want RHACS to help inform that prioritization.



## Network Graph

The Network Graph is a flow diagram, firewall diagram, and firewall rule builder in one.


![Grafana](/OPP-2023-lab-instruction.github.io/images/network.png)


In the Network Graph view, you can configure the type of connections you want to see. In the Flows section (upper left), select:

- Active to view only active connections.

- Allowed to view only allowed network connections.

- All to view both active and allowed network connections.

## Violation

Violations record all of the specific times where a policy criteria has been met by any of the objects in your cluster - images and their components, deployments, runtime activity.

Think of it as the “stream” of events that have occurred, although we don’t want this to just be a “to-do” list for incident response folks.


![Grafana](/OPP-2023-lab-instruction.github.io/images/violations1.png)

Click on any violation, the violation details appear.


![Grafana](/OPP-2023-lab-instruction.github.io/images/violation2.png)


## Compliance Operator

Compliance Operator allows OpenShift Container Platform administrators to define the desired compliance state of a cluster and provides an overview of gaps and ways to remediate any non-compliant policy.
The  Compliance Operator assesses both Kubernetes API resources and OpenShift Container Platform resources, as well as the nodes running the cluster. The Compliance Operator uses OpenSCAP, a NIST-certified tool, to scan and enforce security policies provided by the content.

Click on "Scan Environnement"


![Grafana](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Configuration Management

With Configuration Management, provides efficient configuration management that combines all these distributed entities on a single page. It brings together information about all your clusters, namespaces, nodes, deployments, images, secrets, users, groups, service accounts, and roles in a single Configuration Management view, helping you visualize different entities and the connections between them.


## Policy Management

With Policy Management, RHACS allows you to use out-of-the-box security policies and define custom multi-factor policies for your container environment.
Configuring these policies enables you to automatically prevent high-risk service deployments in your environment and respond to runtime security incidents.


![Grafana](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


All of the policies that ship with the product are designed with the goal of providing targeted remediation that improves security hardening.

You’ll see this list contains many Build and Deploy time policies to catch misconfigurations early in the pipeline, but also Runtime policies that point back to specific hardening recommendations.

These policies come from us at Red Hat - our expertise, our interpretation of industry best practice, and our interpretation of common compliance standards, but you can modify them or create your own.




