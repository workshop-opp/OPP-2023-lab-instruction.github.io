---
title: "CVE Management"
draft: false
weight: 2
---

#Context :

The IT Security team received an alert regarding a new critical vulnerability (CVE) that could have a significant impact on systems. This CVE affects several applications. To avoid potential exploitation of this vulnerability, it is crucial to detect and prevent any new application deployments that may contain it.

# Objective of the exercise:

The main objective is to implement a security policy that blocks any application deployment containing the identified CVE on the affected cluster. This policy must be automated to prevent any risk of unintentional deployment of a vulnerable application.

# Exercise Steps:

Access the RHACS interface and go to the Vulnerability Management section. This interface gives you visibility on all images belonging to your scope.

# Up to you

From these different dashboards we ask you to find and export all the deployments affected by the CVE in PDF format.

Once this step is completed. Go to Platform Configuration > Policy Management and click Create Policy. You fill out the form so that all images with the CVE `CVE X` are blocked during Stage Build and Deploy with an Inform and Enforce response method.

# Solution


{{%expand "Solution: Export the list of deployments affected by CVE CVE-X" %}}

Click Application and Infrastructure, then Deployment. In the filter bar write CVE then the number of our CVE

You will then see all the deployments affected by our vulnerability appear. Then click Export at the top left to export a PDF containing all the information.

{{% /develop%}}

{{%expand "Solution: Creating the policy" %}}


