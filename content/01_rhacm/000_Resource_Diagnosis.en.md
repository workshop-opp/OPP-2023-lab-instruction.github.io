---
title: "Resource Diagnosis"
draft: false
weight: 1
---


## Contexte :

Dans notre environnement de cluster de production, nous avons récemment rencontré un problème critique lié à l'allocation excessive de ressources par l'une des équipes. Cela a conduit à un engagement de requêtes CPU dépassant 300%. Cette situation compromet la disponibilité et la stabilité de notre infrastructure, nécessitant une identification rapide du namespace surchargé et la mise en place de mesures de contrôle des quotas pour prévenir de futurs incidents.

## Objectif de l'exercice :

L'objectif de cet exercice est de détecter le namespace responsable de l'attribution excessive de quotas de ressources et de mettre en place des ResourceQuotas pour prévenir de tels dépassements à l'avenir.

## Étapes de l'exercice :

Accédez au cluster de production et recueillez des informations sur l'utilisation des ressources.

Pour cela rendez-vous dans la section Infrastructure et cliquez sur Grafana (en haut a gauche).

![Grafana](/OPP-2023-lab-instruction.github.io/images/grafana-access.png)

Un certain nombre de dashboard sont present par defaut lors de l'installation de l'observability. Pour y acceder cliquer sur Dashboards puis Browse.

![Dashboard](/OPP-2023-lab-instruction.github.io/images/browse-dashboard.png)

## A vous de jouer 

A partir de ces differents dashboard nous vous demandont de retrouver quelle namespace a un quota CPU surevalue. Lorsque vous aurez trouve le nom du namesapce appliquer lui un resource quota pour empecher la surallocation. En appliquant le manifest suivant :

```shell
oc patch deployment <deployment-name> -p '{"spec":{"template":{"spec":{"containers":[{"name":"<deployment-name>","resources":{"requests":{"cpu":"1"}}}]}}}}' -n <namespace-name>
```




