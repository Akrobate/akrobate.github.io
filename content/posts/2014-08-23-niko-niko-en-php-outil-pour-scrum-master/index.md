---
date: '2014-08-23T14:05:20+02:00'
draft: false
title: Niko Niko en PHP outil pour Scrum Master
slug: niko-niko-outil-scrum-master
tags:
  - php
  - scrum
categories:
  - Web
cover:
  image: "nikoniko-php-calendrier-average-small.avif"
  alt: "Image d'illustration"
description: 
showTOC: true
---

![](nikoniko-php-calendrier-average-small.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](nikoniko-php-graphique-average-small.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Le **Niko Niko** est un **idéophone japonnais** qui vise à rendre compte de la **sensation ou de l'émotion d'un sourire**. C'est aussi le nom donné à un **outil** couramment utilisé dans les organisations **Scrum** visant a donner l'indication de l'humeur et de l’évolution de l'**humeur d'une équipe** sur un laps de temps donné (durée d'un sprint généralement). En pratique le Niko Niko se déroule de manière très **simple et pragmatique**: Sur un calendrier représentant un mois par page, chaque équipier est convié à y inscrire (anonymement) son humeur sous forme d'un smiley en fin de journée. Puis lors des rétrospectives l'indicateur Niko Niko peut révéler des informations intéressantes. En effet il est souvent facile de constater des corrélations, parfois des **causalités entre divers événements projets et l'humeur de l'équipe**.


## Présentation de l'outil NikoNiko PHP
  
Je vous présente un outil écrit en php que vous allez pouvoir installer sur vos serveurs afin de **simplifier la gestion de l'outil NikoNiko** dans votre équipe Scrum. Ce script fonctionne couplé avec une adresse mail gmail qui devra être dédiée à cet effet. Cette adresse mail va servir de boîte de réception pour les smileys des utilisateurs. Il suffira d'envoyer :-) a cette adresse pour que votre smiley soit automatiquement ajouté au calendrier. Un fichier texte descripteur des équipes vous permettra de configurer qui a le droit de participer et a quelles équipes appartiennent les membres. L'identification des utilisateurs se fait par leur adresse mail et bien évidement pour qu'un smiley soit pris en compte sur le calendrier il s'agira d'envoyer le smiley depuis une adresse connue par le script NikoNiko.  


### Fonctionnalités de l'outil Niko Niko PHP.  

- **Anonymisation** des participations
- Ajout de Smiley du jour **par mail** (et anomalies)
- **Relance** de fin de journée à tous ceux qui ont pas encore participé
- Visualisation du calendrier **détail et moyennes**
- Visualisation de la **courbe d'humeur** sur le dernier mois
- Gestion multiéquipe
- **Restriction** de la partie frontale **par IP** 

  
### Prérequis pour faire fonctionner le script NikoNikoPhp.  

- Hébergement **php et mysql** ou **serveur dédié**
- Adresse (g)mail dédié au NikoNiko


{{% gallery %}}

![](nikoniko-php-calendrier-average-small-2.avif)
{ mode="lightbox" miniature-width=200 }

![](nikoniko-php-calendrier-average-small.avif)
{ mode="lightbox" miniature-width=200 }

![](nikoniko-php-graphique-average-small.avif)
{ mode="lightbox" miniature-width=200 }

![](nikoniko-php-calendrier-all.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}

![](nikoniko-php-graphique.avif)
{ mode="lightbox" }


## Installer et configurer le programme NikoNiko PHP
  
Avant toute chose commencez par récupérer le code source du programme en téléchargeant la dernière version:  
  
[Télécharger NikoNikoPhp](http://artiom21.free.fr/projets/nikonikophp/latest.zip)  
  
ou bien en checkoutant depuis svn:  
  
```bash
svn checkout http://niko-niko.googlecode.com/svn/trunk/ niko-niko-read-only
```
  
Une fois que vous disposez des fichiers copiez les sur votre serveur (ou hébergement).  
  

## Création de la base de données mysql et configuration du script
  
A la racine des fichiers que vous avez téléchargé vous trouverez un fichier `niko-niko.sql` contenant le code **sql de la création des tables** de la base de données nécessaire pour le nikonikophp. Exécutez ce script sur la base de donnée mysql que vous avez crée pour le nikoniko. Maintenant copiez ou renommez le fichier `/config/db.sample.php` en `/config/db.php` et renseignez les bonnes **valeurs pour l'accès a votre base de données** (host / user / password)  
  
  
## Configuration de l'équipe et des utilisateurs**  
  
Le droit de participer a un NikoNiko est definit par un fichier config/team.config.ini Ce fichier décrit équipe par équipe les membres qui ont le droit de participer  

```ini
["Team Name"]
teamname = "Informatique"
teamid = "1"
member[] = "membre1@domaine.com"
member[] = "membre2@domaine.com"
member[] = "membre3@domaine.com"
member[] = "membre4@domaine.com"
```

Cet exemple montre la configuration pour une équipe, il va de sois que si vous voulez créer une autre équipe il suffit de duppliquer ce bloc dans le même fichier en incrémentant teamid et en changeant le nom de teamname  

_Pour information : un membre peut être présent dans plusieurs équipes, mais son vote reste unique. En clair un utilisateur présent dans plusieurs équipes ne peut voter qu'une seule fois, cependant son vote influe le calcul des moyennes de chacune des équipes._  


## Configuration de la boite mail

Dans cette toute première version le code est adapté pour fonctionner avec une adresse mail gmail. Il n'y à priori que très peu de modifications a apporter pour que n'importe quelle boite mail puisse fonctionner avec le NikoNikoPHP. Pour le moment cette première version fonctionnera uniquement avec une adresse gmail.  
Donc une fois muni de votre boite gmail dédié au nikoniko copiez le fichier `conf/mail.sample.php` en `conf/mail.php` en modifiant les valeurs `MAIL_USER` et `MAIL_PASSWORD`. Vous ne devriez pas avoir besoin de toucher a `MAIL_HOST` si vous utilisez une boite gmail.  


## Configuration du cron de relance
  
Le cron de relance est une fonctionnalité que je vous propose dans le NikoNiko qui vous permet de relancer l'ensemble des participants du nikoniko n'ayant pas encore voté ce jour. Le fichier à exécuter pour que la relance soit fait se trouve à la racine et s'appelle cron-script.php il vous suffit de créer un appel a ce fichier dans votre [crontab](http://fr.wikipedia.org/wiki/Crontab) à l'heure à laquelle vous voulez effectuer votre relance.  
  
  
## Configuration de l’accès a la visualisation du nikonikophp
  
Le script NikoNiko est accessible en visualisation pour tous, ce qui peut être embêtant pour les hébergements publics. C'est pourquoi dans le dossier config vous avez un fichier: access.config.ini permettant de restreindre l'acces en visualisation du calendrier a certaines IP.  
  
exemple:  

```ini
["access"]
allowAdr[] = "192.168.0.14"
allowAdr[] = "127.0.0.1"
```
  
Cela autorise seulement ces 2 adresses a consulter le calendrier NikoNiko. Si vous souhaitez que tout le monde puisse y accéder sans restriction (car vous avec installé ce script sur l'intranet de l'entreprise par exemple) vous pouvez simplement mettre la valeur `allowAdr[] = "all"` (valeur par défaut lors de l'installation)
