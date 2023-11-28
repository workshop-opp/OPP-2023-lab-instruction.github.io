---
title: "Resource Diagnosis"
draft: false
weight: 1
---


## Contexte :

Dans notre environnement de cluster de production, nous avons récemment rencontré un problème critique lié à l'allocation excessive de ressources par l'une des équipes. Cela a conduit à un engagement de requêtes CPU dépassant 300%. Cette situation compromet la disponibilité et la stabilité de notre infrastructure, nécessitant une identification rapide du namespace surchargé et la mise en place de mesures de contrôle des quotas pour prévenir de futurs incidents.

## Objectif de l'exercice :

L'objectif de cet exercice est de détecter le namespace et le deployment responsable de l'attribution excessive de cpu request et de le patcher.

## Étapes de l'exercice :

Accédez au cluster de production et recueillez des informations sur l'utilisation des ressources.

Pour cela rendez-vous dans la section Infrastructure et cliquez sur Grafana (en haut a gauche).

![Grafana](/OPP-2023-lab-instruction.github.io/images/grafana-access.png)

Un certain nombre de dashboard sont present par defaut lors de l'installation de l'observability. Pour y acceder cliquer sur Dashboards puis Browse.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/browse-dashboard.png)

## A vous de jouer 

A partir de ces differents dashboard nous vous demandont de retrouver quel est le deployment dont la CPU request a ete surevalue par erreur (100 cpu au lieu de 100 milli-cpu). Lorsque vous aurez trouve le nom du namesapce appliquer lui le patch suivant pour remedier a la surallocation : 

```shell
oc patch deployment <deployment-name> -p '{"spec":{"template":{"spec":{"containers":[{"name":"<deployment-name>","resources":{"requests":{"cpu":"10m"}}}]}}}}' -n <namespace-name>
```

## Solution

{{%expand "Solution" %}}

Le tableau des quotas CPU est disponible dans le Dashboard General/Kubernetes/Compute Resources/Cluster. Une fois dans ce dashboard selectionnez le Cluster sno-prod. Dans le Tableau Cpu Quota cliquez sur CPU Requests pour les trier dans l'ordres. Vous devriez alors observer que le namespace Mirage dispose d'une request de 100 cpu alors qu'il n'en use que 0.001. C'est donc le namesapce problematique.

{{% /expand%}}











