---
title: "Resource Diagnosis"
draft: false
weight: 1
---

## Goal:
Resolve deployment failure caused by quota limitations and successfully deploy the application by adjusting OpenShift quotas.

## Actions:
Attempt to deploy the application in OpenShift.

Use 
```shell
oc new-app <application_manifest> to initiate deployment.
```
Click on the "Deploy" button in the OpenShift console.
Identify resource constraints in RHACM's Grafana.

Access RHACM's Grafana dashboard.
Select the cluster, navigate to "Observability" > "Grafana".
Observe resource utilization metrics.
Confirm quota issues impacting deployment.

Review Grafana metrics indicating resource constraints.
Adjust quotas in OpenShift.

Locate "Resource Quotas" in the OpenShift console.
Edit the specific quota impacted by the deployment issue.
Increase resource limits as needed.
Redeploy the application.

Use 
```
oc rollout latest <application_deployment> 
```
for redeployment.
Monitor deployment status for successful completion.