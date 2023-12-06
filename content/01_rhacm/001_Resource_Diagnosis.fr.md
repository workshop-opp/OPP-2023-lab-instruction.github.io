---
title: "Observability"
draft: true
weight: 0
---


## Contexte 

Dans notre environnement de cluster de production, nous avons récemment rencontré un problème critique lié à l'allocation excessive de ressources par l'une des équipes. Cela a conduit à un engagement de requêtes CPU dépassant 300%. Cette situation compromet la disponibilité et la stabilité de notre infrastructure, nécessitant une identification rapide du namespace suralloué.

## Objectif de l'exercice 

L'objectif de cet exercice est de détecter le namespace et le deployment responsable de l'attribution excessive de cpu request et de le patcher.

## Étapes de l'exercice 

Accédez au cluster de hub et recueillez des informations sur l'utilisation des ressources.

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


![Dashboard](/OPP-2023-lab-instruction.github.io/images/tableau-cpu.png)

Connectez vous au cluster sno-prod et rendez vous dans le namespace mirage. Cliquez sur Workloads > Pods. On observe que le pods todo-app est au statut Pending car les noeuds de dispose pas d'assez de resources pour repondre a notre request. On observe que le Deployement qui lui est associe est todo-app. Il ne nous reste donc plus qu'a appliquer le patch suivant.

![Request](/OPP-2023-lab-instruction.github.io/images/resource-request.png)

```shell
oc patch deployment todo-app -p '{"spec":{"template":{"spec":{"containers":[{"name":"todo-app","resources":{"requests":{"cpu":"10m"}}}]}}}}' -n mirage
```

{{% /expand%}}











