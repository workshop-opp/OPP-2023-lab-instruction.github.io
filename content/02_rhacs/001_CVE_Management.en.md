---
title: "CVE Management"
draft: false
weight: 2
---

## Context

The IT Security team received an alert regarding a new critical vulnerability (CVE) that could have a significant impact on systems. This CVE affects several applications. To prevent potential exploitation of this vulnerability, it is crucial to detect and prevent any new application deployments that may contain it.

## Objective of the exercise

The main objective is to implement a security policy that blocks any application deployment containing the identified CVE on the affected cluster. This policy must be automated to prevent any risk of unintentional deployment of a vulnerable application.

## Exercise steps

Access the RHACS interface and go to the Vulnerability Management section. This interface gives you visibility over all the images belonging to your scope.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/dashboard-vulnerability-management.png)


## Up to you

From these different dashboards we ask you to find and export all the deployments affected by CVE in PDF format.

Once this step is completed. Go to Platform Configuration > Policy Management and click Create Policy. You will fill out the form so that all images with the CVE `CVE-2022-32207` are blocked during Stage Build and Deploy with an `Inform and Enforce` method.

The policy must meet the following criterion:

| Parameters | Value |
|---------|---------|
| Name | **policy-<YOUR_CITY>** |
| Categories | Vulnerability Management |
| Lifecycle internships | Build and Deploy |
| Response method | Inform and enforce |
| Restrict-by-scope | **<YOUR_CITY>-ns** |
| Cluster-scope | local-cluster |
|---------|---------|

## Solution


{{%expand "Solution: Export the list of Deployments affected by the CVE `CVE-2022-32207` " %}}

Click Application and Infrastructure, then click Deployment.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/dashboard.png)

In the filter bar write CVE then the CVE number.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/peloton.png)

You will then see all the deployments affected by our vulnerability appear. Then click Export at the top right to export a PDF containing all the information.

{{% /expand%}}

{{%expand "Solution: Policy Creation" %}}

![Policy-1](/OPP-2023-lab-instruction.github.io/images/create-policy-step-1.png)

![Policy-2](/OPP-2023-lab-instruction.github.io/images/create-policy-step-2.png)

![Policy-3](/OPP-2023-lab-instruction.github.io/images/create-policy-step-3.png)

![Policy-4](/OPP-2023-lab-instruction.github.io/images/create-policy-step-4.png)

TODO: Add manifest to validate

{{% /expand%}}