---
date: '2012-05-19T14:05:20+02:00'
draft: false
title: Capteur de lignes pour la robotique et librairie arduino
slug: capteur-lignes-pour-robotique-et-librairie-arduino
tags:
  - arduino
  - capteur de lignes
  - electronique
  - lego
  - robot
  - robotique
categories:
  - Électronique
cover:
  image: capteur-de-lignes-pour-robot-boitier-lego.avif
  alt: "Image d'illustration"
description: 
showTOC: true
---


![](capteur-de-lignes-pour-robot-boitier-lego.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Un capteur de lignes permet de détecter une variation d'intensité lumineuse sur une surface. Il s'agit de permettre la détection de lignes noires tracées sur une feuille blanche, ou tout autre variation de couleurs à condition que le contraste entre les deux couleurs soit suffisant.  

Les capteurs de lignes peuvent être infrarouges ou alors fonctionnant avec la lumière visible. Dans le cadre de cet article je vous propose que réaliser un capteur avec une photo résistance et un éclairage par une diode électroluminescente haute luminosité, donc a lumière visible. Ce genre de capteurs est sensible aux variations de lumière ambiante. Il est possible évidement d'essayer de créer une sorte de boite noire autour du capteur afin qu'il ne soit pas perturbé par la lumière ambiante, mais cela sous entends que votre boite de capteur devra être au ras du sol et cela n'est pas toujours facile à faire. Pour pallier à ce problème nous allons utiliser un algorithme qui permettra au robot ou tout autre dispositif de calculer un seuil de détection dynamique.  

J'ai choisi d'utiliser des pièces de lego pour créer le boitier qui portera les deux composants. En effet dans l'utilisation que je souhaite en faire c'est nécessaire car ce capteur sera fixé sur un robot détecteur de lignes à base d'arduino. Le schémas électronique est très simple. Le composant obtenu comporte trois fils. Une alimentation, une masse et le signal qui représente une tension correspondant a l'intensité lumineuse de la surface observée par le capteur de lignes.  

![](schemas-capteur-de-lignes.avif)
{ mode="lightbox" }

  
## Librairie pour le capteur de lignes sur Arduino
  
Maintenant que la partie mécanique et électronique du montage est faite il s'agit de voir comment transformer les variations de lumière en détection de ligne. Je propose la classe suivant pour arduino qui permet d'effectuer la détéction de ligne par ce type de capteurs, et qui s'adapte a la lumière ambiante.  
  
Fichier prototype LineSensor.h  
  
```cpp
/*
  LineSensor.h - Driver pour le suivi de lignes
  Created by Artiom FEDOROV Mai 2012
  Released into the public domain.
*/

#ifndef LineSensor_h
#define LineSensor_h

#include "Arduino.h"

class LineSensor
{
 public:
  LineSensor(int pin);
  int checkLine();
  
 private:
 
  int _minV;
  int _maxV;
  int _pin;
};

#endif
```

  
Fichier source LineSensor.cpp  
  
```cpp
#include "Arduino.h"
#include "LineSensor.h"

LineSensor::LineSensor(int pin) {
  _minV = -1;
  _maxV = -1;
  _pin = pin;
  pinMode(pin, INPUT);
}

int LineSensor::checkLine() {
  int value = analogRead(_pin);

  if (_minV == -1) {
     _minV = value; 
  }
 
  if (_maxV == -1) {
     _maxV = value; 
  }
 
  if (value <= _minV) {
    _minV = value;
  }
 
  if (value >= _maxV) {
     _maxV = value; 
  }
 
  if (value < (((_maxV-_minV) / 1.5) + _minV)) {
    return 1;
  } else {
    return 0; 
  }
} 
```


## Utiliser la librairie sur un arduino

![](capteur-de-lignes-en-fonctionnement.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Pour utiliser cette lib, rien de plus simple. Vous devez tout d'abord inclure le fichier LineSensor.h dans votre fichier principal. Les fichiers LineSensor.h et LineSensor.cpp devront se trouver à côté de votre fichier principal. Ensuite il vous suffit de déclarer l'objet LineSensor avec comme paramètre au contructeur le numéro de pin de votre carte arduino (ou teensy). Ensuite il vous suffit de faire appel a la méthode checkLine() afin de savoir si le capteur détecte une ligne en ce moment ou pas.  
  
## Documents annexe
  
- [Archive LineSensor class](http://artiom21.free.fr/projets/arduino-linesensor-lib/LineSensor-arduino-lib.zip)  
  