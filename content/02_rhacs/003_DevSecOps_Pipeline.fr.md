---
title: "DevSecOps Pipeline"
draft: false
weight: 4
---

Dans cette partie, nous allons voir comment RHACS peut totalement s'intègrer dans une approche DevSecOps.

Pour cela, nous avons un pipeline à disposition qui à pour objectif de déployer une application sur notre cluster.

L'objectif de ce pipeline est simplement de git clone un dépôt, build l'image et la déployer.
Entre l'étape du build et du déploiement, nous avons 2 étapes parallèles : image-scan, image-check.
C'est ici que RHACS intervient.

Ainsi, si RHACS detecté une CVE présente sur l'image de l'application, le déploiement sera bloqué.


Passons à la pratique : 

- Cliquer sur "START"
- Suivez les étapes d'avancement du pipeline

![Pipeline](/OPP-2023-lab-instruction.github.io/images/pipeline_1.png)



Comme vous pouvez le voir, l'étape image-check est bloqué, car RHACS à detecté une violation qui lui ordonne un enforcement du déployement.
C'est pour cela que le pipeline s'est arrêté et l'application n'est pas déployer.


Allons sur le dashboard de RHACS et plus précisement dans la section Violations.


![Violations](/OPP-2023-lab-instruction.github.io/images/pipeline_2.png)

A la 1ère ligne, vous pouvez la policy pillow_policy qui a bloqué le déploiement de notre application.
Vous pouvez cliquer sur la policy pour plus de détail.
Dans notre cas, la policy à bloqué le déploiement car dans l'application que nous souhaitons déployer, il y a bien une CVE.
Cette CVE concerne pillow, une librairie python qui permet de manipuler des images.
Cette CVE existe uniquement sur la version 9.5.0 de pilow, mais elle n'est plus présente sur la version la plus récente.

Dans un autre contexte, le développeur devra mettre à jour sa librairie, réaliser les tests unitaires, d'intégrations pour vérifier si cette mise à jour n'infecte pas le comportement de l'application.

Ensuite, il devra relancer le pipeline pour déployer la nouvelle version de l'application.

Dans notre cas, pour explorer les fonctionnalités de RHACS, nous allons directement agir sur notre dashboard RHACS.

Pour cela, nous allons indiquer qu'on ne souhaite plus bloquer le déployement de notre application à cause de notre CVE.
RHACS se contentera simplement de nous informer qu'une CVE est présente sur notre application rien de plus.

Suivez les étapes :

- Cliquez sur Platform Configuration
- Policy Management
- Cliquez sur la barre de recherche "Filter policies", sélectionner "Policy"
- Tapez "pillow_policy", il s'agit de la policy qui ordonne le blocage du déploiement de notre application.
- Cliquer sur la policy
- en haut à gauche, cliquez sur Actions, puis edit policy.
- Allez directement à section 2 : Policy Behavior

![policy](/OPP-2023-lab-instruction.github.io/images/pipeline_3.png)

Dans la section "Response method" comme ci dessus, "inform and enforce" est coché.

- Cochez "inform"
- Cliquez sur Next jusqu'à qu'on vont proposer de sauvegarder la policy.
- Sauvegarder les modifications


Maintenant, retournez sur votre pipeline et relancez un run.

Comme vous pouvez le voir, l'application est deployé sur le cluster, sans que RHACS bloque le déploiement.
Cependant, si vous retounez sur le dashboard, RHACS vous informe uniquement de nouveau qu'une CVE est présente dans votre application.






