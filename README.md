# sdd-poc-deployment

# Déploiement de l'application
From https://github.com/InseeFrLab/sspcloud-tutorials/blob/main/deployment/shiny-app.md

## Création d'un Chart Helm
Le déploiement de l'application nécessite la création d'un chart Helm. Concrètement, un chart Helm peut être vu comme un package Kubernetes, contenant les ressources nécessaires au déploiement d'une application.

Le dépôt de déploiement contient un chart Helm permettant le déploiement de l'application template. Il convient donc de forker également ce second repository, qui va servir de base pour le chart Helm de votre application. Ce chart contient pour l'essentiel deux fichiers.

Le fichier Chart.yaml contient les métadonnées du chart (nom, version) ainsi que ses dépendances, i.e. les potentiels autres charts Helm dont il hérite. Dans notre cas, on voit que le chart hérite du chart Shiny d'InseeFrLab. Ce dernier chart, plus complexe, spécifie généralement les ressources Kubernetes nécessaires au déploiement d'une application Shiny, de sorte à ce que l'on ait qu'à modifier les valeurs d'instanciation pour déployer notre application.

Le fichier values.yaml contient précisément les valeurs que l'on modifie par rapport au chart général (parent). Les modifications à apporter dépendent naturellement de ce que réalise en pratique l'application, car cela conditionne les ressources dont elle a besoin. Dans un premier temps, il nous faut modifier :
- le chemin et nom de l'image
- le tag de l'image. Il s'agit du tag de l'image sur le DockerHub. Par défault, et pendant la phase de développement, on peut indiquer le tag latest pour signifier "la dernière version de l'image qui a été produite". Lorsque l'application est en production, il est préférable d
- l'hostname de l'Ingress, i.e. l'URL à laquelle l'application sera accessible une fois déployée. Cette URL doit être de la forme *.lab.sspcloud.fr ; par exemple dans notre cas : myshinyapp.lab.sspcloud.fr.
