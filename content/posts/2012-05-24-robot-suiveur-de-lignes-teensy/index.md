---
date: '2012-05-24T14:05:20+02:00'
draft: false
title: "Robot suiveur de lignes a base du teensy (arduino)"
slug: "robot-suiveur-de-lignes-teensy"
tags:
  - arduino
  - capteur de lignes
  - electronique
  - informatique
  - robot
  - robot suiveur de lignes
  - robotique
  - teensy
  - telecommande lego
categories:
  - Robotique
showTOC: true
cover:
  image: "robot-suiveur-de-lignes-main.avif"
  alt: "Image d'illustration"
description: Découvrez comment fabriquer un robot suiveur de lignes autonome piloté par un microcontrôleur Teensy (Arduino), avec un châssis Lego Technic et des moteurs contrôlés par infrarouge. Tutoriel complet avec code source, schémas électroniques et explications.
---

![](robot-suiveur-de-lignes-main.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](P1010040.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Le **robot suiveur de lignes** est un petit projet très simple. On trace une ligne au feutre noir sur une grande feuille blanche on pose le robot sur la ligne, et ce dernier va suivre la ligne. Ici mon robot fonctionne avec un Teensy 2 ++ (équivalent de l'**arduino** mais avec des ports entrés/sorties en plus) cadencé a **16Mhz**. Le châssis utilisé est en légos technics, et pour la motorisation j'ai utilisé les **moteurs lego** power functions. Les lignes sont détectées grâce a deux **capteurs de lignes** basés sur des photo résistance. L'astuce principale de ce robot réside dans l'**utilisation de l'infrarouge pour commander les moteurs** officiels légo. Cela permet de ne pas avoir la moindre interface "physique" entre le circuit contrôleur et l'étage de la motorisation. Le robot suiveur de lignes possede donc deux parties electroniques distinctes. D'un coté les lego power functions (motorisation légo), et de l'autre le circuit de la plaque a essai qui est alimenté par une batterie de 9v.


## Le châssis et les capteurs

Le châssis est entièrement réalisé en lego technics issus du set 8275. C'est un bulldozer de lego technics. Ce set comprenait pas mal de pièces intéressantes pour la robotique: 4 moteurs deux récepteurs infrarouges, un pack alimentation et une télécommande infrarouge. Par ailleurs étant donné qu'il s'agit d'un bulldozer le set comprends des chenilles très pratiques pour la motorisation. Pour commander cette base en légo j'émule les signaux de la télécommande officielle en utilisant ma classe arduino LegoRC. Je vous invite a lire l'article sur la [télécommande lego power function et librairie arduino](http://artiom-fedorov.blogspot.fr/2012/05/telecommande-infrarouge-lego-power.html) pour mieux comprendre les détail de l'interface. Donc l'interface entre l'arduino et le châssis lego se limite a une diode infrarouge orientée vers le récepteur lego power functions.  
Les capteurs de lignes sont simplifiés au maximum. En effet il ne s'agit que d'une simple photo résistance et une diode d'éclairage. Je vous invite aussi a lire l'[article sur ce capteur de lignes](http://artiom-fedorov.blogspot.fr/2012/05/capteur-de-lignes-pour-la-robotique-et.html), et surtout la classe LineSensor pour arduino, qui permet d'utiliser très simlement ce capteur.  
En ce qui concerne la fixation de la plaque a essai le hasard fait bien les choses ci bien que une des fixations standard de légo rentre pile poil dans les quartes trous dont la plaque a essai est munie. C'est une [plaque a essai relativement basique achetée chez SELECTRONIC](http://www.selectronic.fr/plaque-d-essais-550-points.html).


## Quelques photos du robot

{{% gallery %}}

![](P1010052.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010053.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010055.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010054.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010042.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010041.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010040.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010039.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010038.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010037.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Le programme informatique
  
Le programme informatique pour l'arduino est très simple. On commence par déclarer les capteurs avec en paramètre la broche sur laquelle est branché le capteur. Ensuite on déclare l'objet LegoRC qui permet de communiquer simplement avec les moteurs. Dans la boucle principale on vérifie les capteurs. Si les deux capteurs ne détectent pas de ligne alors le robot avance. Si un des capteurs est actif alors le robot pivote sur lui meme jusqu'a ce que le capteur ne detecte plus à nouveau la ligne.  
  

```cpp
#include "LineSensor.h"
#include "LegoRC.h"

LineSensor rightLineSensor(38);
LineSensor leftLineSensor(39);

LegoRC legoRC(45, 50);

void setup() {
}

void loop() {
  int mspeed = 3;  // Minimum 1, maximum 7
  int rv = rightLineSensor.checkLine();
  int lv = leftLineSensor.checkLine();
 
  if ((rv == 0) && (lv == 0)) {
    legoRC.sendCommand(4, mspeed, (16 - mspeed)%16 );
  }
 
  if (rv == 1) {
    legoRC.sendCommand(4, (16 - mspeed)%16, (16 - mspeed)%16);     
  }

  if (lv == 1) {
    legoRC.sendCommand(4, mspeed, mspeed);      
  } 
}
```
  
  
## L'electronique : schemas
  
Le schémas électronique du robot est on ne peut plus simple. Le montage utilise un teensy2++ équivalent de l'arduino. Le schémas électronique proposé ci dessous utilise le brochage déclaré dans le programme du robot. Sur le schémas vous pouvez voir la partie alimentation a base d'un 7805 standart. En effet l'alimentation de la carte est assuré par une batterie de 9v. On n'utilise pas ici l'alimentation des moteurs. Notre carte a sa propre partie alimentation.  



![](RobotLineFollower.avif)
{ mode="lightbox" }
  
  
## Planning de gant du projet Robot suiveur de lignes
  
Enfin pour finir, un petit bonnus: J'utilise souvent pour encadrer mes projets le diagramme de gant qui permet de lister les tâches à réaliser puis de déterminer l'enchainement des tâches. Le diagramme de gant permet de s'organiser rapidement et savoir par quoi commencer en fonction des enchainements possibles une fois une tache achevée. Je vous invite a vous renseigner sur cette méthode d'organisation qui permet d'être plus efficace dans des projets ayant de nombreux axes de développement.  
  

![](gant-diagram-robot.avif)
{ mode="lightbox" }


## Vidéo du robot en fonctionnement

{{< youtube-lite "IvgFzfjKfoU" >}}


## Documents annexes
  
- [Code source complet du projet robot suiveur de lignes arduino](http://artiom21.free.fr/projets/arduino-robot-line-follower/RobotLineFollow.zip)  
- [Documentation sur l'interface arduino - lego (LegoRC arduino class)]({{< relref "posts/2012-05-21-telecommande-infrarouge-lego-power-function-et-librairie-arduino/index.md" >}})
- [Documentation sur les capteurs de lignes et classe arduino](http://artiom-fedorov.blogspot.fr/2012/05/capteur-de-lignes-pour-la-robotique-et.html)
