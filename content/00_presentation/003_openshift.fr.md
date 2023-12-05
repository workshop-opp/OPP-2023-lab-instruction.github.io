---
title: "OpenShift"
draft: false
weight: 4
---

## OpenShift cluster

3 clusters OpenShift sont déjà déployés via l'environnement **RHPDS** et le service **"AWS Blank Open Environemnt"** :

* Cluster Hub
* Cluster de développement SNO
* Cluster de production SNO

**Aucune action n'est requise de votre part.**

![Service RHPDS](/OPP-2023-lab-instruction.github.io/images/aws-blank-open.png)


## Détails du cluster OpenShift

* **URL de la console du cluster OCP :** `https://console-openshift-console.apps.workshop-opp.sandbox2156.opentlc.com`

* **URL de l'API du cluster OCP :** `https://api.workshop-opp.sandbox2156.opentlc.com:6443`

Il existe un utilisateur OpenShift dédié pour chaque utilisateur.


{{% notice tip %}}
Votre instructeur vous fournira votre identifiant qui correspond à un nom de ville ainsi que votre mot de passe.
{{% /notice %}}


Pour vous connecter à votre cluster Openshift, cliquez sur *URL de la console OCP Cluster* ci-dessus et renseignez votre nom d'utilisateur et votre mot de passe. Vous aurez accès au *Terminal Web* en cliquant sur l'icône **>_** en haut à droite. Le Terminal Web fournit le client *oc*.