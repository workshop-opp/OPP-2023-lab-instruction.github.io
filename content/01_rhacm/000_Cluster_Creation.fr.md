---
title: "Création de cluster"
draft: false
weight: 1
---


## Création de cluster (réalisé par le formateur)

Dans les conditions préalables à ce cours, les informations d'identification AWS ont été créées à partir de la clé d'accès et de la clé secrète.

- Dans le menu de navigation, accédez à Automatiser l'infrastructure > Clusters.


- Sur la page Clusters, cliquez sur Créer un cluster. Et sélectionnez Amazon Web Services. Sélectionnez Standalone.

![Infrastructure RHACM](/OPP-2023-lab-instruction.github.io/images/rhacm-infrastructure.png)

- Nous allons maintenant remplir le formulaire pour créer un cluster avec les détails ci-dessous

| Paramètres | Valeur |
|----------|----------|
| Titre de fournisseur d'infrastructure | informations d'identification AWS |
| Nom du cluster | sno-demo |
| Ensemble de clusters | par défaut |
| Domaine DNS de base | sandbox2156.opentlc.com |
| Image de sortie | OpenShift 4.14.3 |
| Paramètres | Valeur |
|----------|----------|
| Région | eu-west-2 |

![Yaml activé](/OPP-2023-lab-instruction.github.io/images/yaml-on.png)


- Cliquez maintenant sur Suivant, jusqu'à la révision, et enfin cliquez sur Créer.

- Vous pouvez désormais suivre le processus de création du cluster dans l'interface utilisateur RHACM avec les journaux d'installation du cluster.

![[Processus d'installation]](/OPP-2023-lab-instruction.github.io/images/creating-cluster-sno-demo.png)

- À la fin, vous devriez voir votre cluster nouvellement créé dans les états prêts dans l'interface utilisateur.