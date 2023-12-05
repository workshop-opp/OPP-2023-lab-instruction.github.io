---
title: "Walkthrough interface"
draft: false
weight: 1
---


Through this activity, we will quickly see the main features of Red Hat Advanced Cluster Security

## Connection to rhacs

To access rhacs, click on the path menu at the top right and click on `Red Hat Advanced Cluster Security`.

![RHACS connection](/OPP-2023-lab-instruction.github.io/images/rhacs-connection.png)

Select atelier-opp as the authentication provider. Then click on login.

![Login Login](/OPP-2023-lab-instruction.github.io/images/login-workshop-opp.png)

 Authenticate with your username/password provided by the instructor.

## Vulnerability management

Vulnerability management provides a dashboard containing important information on the applications deployed on the cluster. We mainly find the vulnerabilities (CVE included), which are the most widespread or the most recent, from which the Docker images used come. The dashboard also provides the vulnerabilities present within the cluster.


![Vulnerabilities](/OPP-2023-lab-instruction.github.io/images/vuln_manag.png)

  RHACS can scan deployed images and integrates with your registry. RHACS also provides extensive support for third-party scanners such as Anchore, Red Hat Quay, Clair, and Tenable to complement your existing image scanning tools.


## Risk management


Let's take a look at the Risks view, where we go beyond the basics of vulnerabilities to understand how deployment configuration and execution activity affect the likelihood of an exploit occurring.


![Risk](/OPP-2023-lab-instruction.github.io/images/risk.png)


This list displays deployments, across all clusters and namespaces, ordered by risk priority.
The risk is calculated according to the activity of the application, its exposure, the number of deployments and the CVEs present.
The view is ranked in order of priority.
Thus, this functionality will allow you to concentrate your efforts on the deployments that present the most risks.



## Netwokr Graph

The Network Graph is both a flow view and a NetworkPolicy generator.


![Network](/OPP-2023-lab-instruction.github.io/images/network.png)


Network Graph is a functionality for visualizing deployments present on your namespaces.
Thus, this functionality presents you in the form of a flow diagram, the different connections existing on your different pods.
Based on the diagram you can make decisions about adding or removing flows.
The strong point of the Network Graph is that RHACS can generate network policies for you in order to better protect and partition your connection flows.

## Violations

The Violations section is a feature in the form of a register that records all specific moments when a policy created by the security team was not respected in your cluster.

This register allows you, at a glance, to see the policy violations present on your cluster by filtering several pieces of information such as:
- the namespace concerned
- the type: specifies if the vulnerability or policy is present on a deployment, secret, namespace etc...
- enforced: the deployment has been blocked or not
- the level of severity
- the vulnerability category
- when the vulnerability or policy was detected (build, deployment, runtime)
  




![Violations](/OPP-2023-lab-instruction.github.io/images/violations1.png)

Click on any violation to see more details.


![Violation2](/OPP-2023-lab-instruction.github.io/images/violation2.png)


## Compliance Operator

The Compliance Operator provides you with a dashboard that allows you to access defined metrics to see the state of compliance required in certain areas of activity such as banking and medicine.
The Compliance Operator evaluates both Kubernetes API resources and Openshift resources, as well as the nodes running on the cluster.
This feature uses OpenSCAP, a NIST-certified tool, to analyze and enforce security policies provided by content.



Click “Environmental Scan”


![Compliance_Operator](/OPP-2023-lab-instruction.github.io/images/compliance.png)


## Configuration management

Configuration Management, provides efficient configuration management that combines all entities on a single page. It brings together information about all your clusters, namespaces, nodes, deployments, images, secrets, users, groups, service accounts and roles in a single view, helping you visualize different entities and the connections between them.


## Policy management

With policy management, RHACS allows you to use out-of-the-box security policies and define custom multi-factor policies for your container environment.
Configuring these policies allows you to automatically prevent high-risk service deployments in your environment and respond to runtime security incidents.


![Policy](/OPP-2023-lab-instruction.github.io/images/policy_management.png)


All policies provided with the product are designed with the goal of providing targeted corrective actions that improve security hardening.

You will see that this list contains many policies on build and deployment to detect configuration errors (for example in a pipeline), but also execution policies which refer to specific hardening recommendations.