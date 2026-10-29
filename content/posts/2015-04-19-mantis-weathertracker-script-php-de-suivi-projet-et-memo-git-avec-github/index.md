---
date: '2015-04-19T14:05:20+02:00'
draft: false
title: MantisWeatherTracker script PHP de suivi projet et mémo Git avec GitHub
slug: Mantis-weather-tracker-script-php-suivi-projet
tags:
  - API
  - gestion de projet
  - informatique
  - mantisBT
  - php
  - script php
  - SOAP
categories:
  - Web
cover:
  image: "weather_tracker.avif"
  alt: "Image d'illustration"
description: 
showTOC: true
---


### MantisWeatherTracker script PHP de suivi projet et mémo Git avec GitHub

![](weather_tracker.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](mantis-weather.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }


**Mantis Weather Tracker** est un **script PHP** très simple vous permettant d'avoir une vue sous forme de **météo de l'ensemble de vos projets** mantisBT (mantig bug tracker). J'ai codé ce projet il y a quelques temps déjà pour mes propres besoins de suivi de projet. Il m'a semblé important d'avoir une **vue d'ensemble simple et motivante** de tous les projets actuellement actifs.  Le script que j'ai développé s'appuie entièrement sur les API de mantisBT, et ne nécessite aucune configuration particulière. La connexion se fait avec votre login et votre mot de passe mantis.  


Je profite de la migration de ce projet de googleCode vers gitHub pour le présenter brièvement et faire un **petit mémo des quelques commandes essentielles pour travailler avec git sur gitHub**. La migration en sois n'est pas un problème étant donné que google a mis à disposition un bouton d'export vers gitHub. Après cela il faudra cloner vos projets pour avoir les copies du dépot localement. Je vous présente à la fin de l'article le déroulé pour travailler avec git, et les commandes minimales pour y arriver.

## Pourquoi Mantis Weather tracker ?

![Extrait de l'écran de Rapports Mantis Standard](mantis-repport-extact.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }


Le petit projet MantisBT Weather Tracker est un simple tableau de bord pour MantisBT. **Mantis** propose un rapport détaillé de l'ensemble de projet, mais la **lecture de ces tableaux** n'est **pas forcément agréable**. Il est parfois **laborieux de se faire une idée** rapide de l'avancement de ses projets en un rapide clin d'oeil.  
  
Le projet weather tracker est né d'une réelle **nécessite de se faire une idée aussi précise que rapide** de l'état d'**avancement de tous ses projets**.  
  
Ce script est codé sous forme d'un client qui interroge une instance Mantis en SOAP. Vous pouvez utiliser directement vos logins / mot de passe de votre instance Mantis pour obtenir la vue Météo de votre mantis avec MantisWeatherTracker  
  
**MantisWeatherTracker** va scorer l'avancement de chaque projet et le représenter sous une forme ludique et très parlante a tous (la météo) afin de vous **donner une visibilité mantis plus agréable et ergonomique**


## Screenshots du Tableau de board Mantis Weather Tracker

{{% gallery %}}

![Exemple 1 de rapport Météo Mantis Weather Tracker](mantis-weather.avif)
{ mode="lightbox" miniature-width=200 }

![Exemple 2 de rapport Météo Mantis Weather Tracker](Capture-du-2014-01-05-18_41_55.avif)
{ mode="lightbox" miniature-width=200 }

![Ecran de connection Mantis Weather Tracker](Capture-du-2014-01-05-18_42_19.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Description des indicateurs Mantis Weather Tracker**  


![](mantis-weather-global-indicator.avif)
{ .article-image-left mode="lightbox" miniature-width=120 }

La météo du jour est une moyenne des météo de chaque projets. Pour un projet donné la météo du projet est calculé de la façon suivante. On détermine la dernière activité sur chaque projet. La projet dont la dernière modification est la plus ancienne va nous donner l'amplitude pour la plus mauvaise météo. De là on place la météo pour chaque projet en fonction de la recense de la dernière modification. Les scores obtenues vont de 0 à 6.  
  
En gros cela donne

```
score = (NOW() - dateDerniereModifProjet) / Amplitude * 6  
```


![](mantis-weather-oneline-indicator.avif)
{ .article-image-left mode="lightbox" miniature-width=120 }

Le logo a gauche du titre de chaque ligne représente la météo actuelle sur ce projet. En dessous vous avez la représentation du temps écoulé depuis la dernière modification sur le projet. (Il peut s'agir de la création d'un nouveau bug, résolution, commentaire etc etc)  

![](mantis-weather-oneline-bugsrepartition.avif)
{ .article-image-left mode="lightbox" miniature-width=120 }

Ce petit indicateur a droite de chaque ligne reprend l'état des taches. Représente la répartition des taches par status. Les couleurs respectent la légende proposé par défaut par mantisBT.  
  
![](mantis-weather-oneline-completezone.avif)
{ .article-image-left mode="lightbox" miniature-width=120 }

L'état d'avancement global du projet. Il s'agit ici du rapport entre tous les bugs et les bugs en statut résolut.  
pourcentage = nbrResolus / nbrTotal * 100  
  
  
  
## Télécharger le projet MantisWeatherTracker
  
Pour télécharger le projet rendez vous sur GitHub  
  
[https://github.com/Akrobate/mantisbt-weather-tracker](https://github.com/Akrobate/mantisbt-weather-tracker)  
  
  
  
  
  

## **Mémo de travail avec git sur GitHub**


![](logo-git.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](github-logo.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }


Le déroulé général pour travailler avec un projet git. Le projet MantisWeatherTracker sera pris comme exemple dans les commandes.  

1. On clone un projet sur gitHub  
2. On modifie le code source, commits sur les modifs (toujours localement)  
3. On pousse les modifs sur le serveur GitHub

  
### 1. Cloner un projet depuis gitHub
  
Cloner un projet revient a copier son code source et tout l'ensemble du dépôt se voit copié locallement. Cela équivaut à un svn checkout, sauf que la grosse différence réside dans le fait que tout le dépot est copié localement en plus du code source.  

```bash
git clone {URL_CLONE_GITHUB}  
```  

Cette commande va créer un dossier contenant le projet avec le dépôt configuré sur le projet gitHub distant.  
  
  
### 2. Modifier localement le code source
  
A chaque fois qu'on veut commit il suffit de taper git commit. Les commits sous git se font sur le dépôt local, et non distant contrairement au commit de svn. Vous aurez donc une étape supplémentaire pour envoyer toutes vos modifs sur le dépot gitHub de votre projet.  
  
A chaque fois que vous souhaiter commiter tape:  
  
```bash
git commit -m "message que vous voulez rajouter au log"  
```
  
### 3. On pousse les modifs sur le serveur GitHub
  
Puis pour envoyer l'ensemble de vos commit sur le dépot de votre projet gitHub tapez:  

```bash
git push  
```
  
### Quelques commande très utiles en plus
  
Pour récupérer les modifications distantes depuis gitHub

```bash
git pull  
```

Pour connaître les fichiers modifiés entre le code et le dépôt local  

```bash
git status  
```

Pour voir les différences  

```bash
git diff {votrefichier}
```