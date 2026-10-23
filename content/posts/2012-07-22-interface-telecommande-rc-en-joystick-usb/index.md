---
date: '2012-07-22T14:05:20+02:00'
draft: false
title: "Interface télécommande RC en Joystick USB"
slug: "interface-telecommande-rc-joystick-usb"
tags:
  - arduino
  - electronique
  - informatique
  - servo moteur
  - teensy
  - telecommande RC
categories:
  - Électronique
  - RC
cover:
  image: "P1010424.avif"
  alt: "Image d'illustration"
description: Créez un adaptateur USB pour votre télécommande RC avec Arduino/Teensy. Pilotez vos simulateurs de vol sur PC sans fil via le récepteur radio.
author: Artiom FEDOROV
ShowToc: true
---

![](P1010424.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](P1010400.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

L'idée de ce projet est de pouvoir **adapter n'importe quelle télécommande de modélisme sur un ordinateur** par le biais du port **USB**. Côté ordinateur, rien d'extraordinaire, on veut simplement obtenir un nouveau **périphérique de type joystick**. Dans mon projet j'utilise une télécommande 4 voies, de ce fait l'adaptateur va "faire croire" (émuler) à l'ordinateur la présence d'un joystick USB 4 axes. La particularité de l'adaptateur vient du fait qu'au lieux d'utiliser la prise écolage sur la télécommande, nous utilisons simplement le récepteur de la télécommande (ou un récepteur compatible à la même fréquence). Ce sont donc les signaux reçus par le récepteur qui seront traités par l'adaptateur. Ce procédé à un avantage incontestable qui est celui de vous offrir la possibilité de vous servir de votre télécommande (sans fils) pour piloter un modèle dans FMS ou votre simulateur ou jeu favoris.

  
## Montage électronique

![](P1010403.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](P1010409.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

La partie électronique du montage se limite à un seul composant principal: le teensy2++ (équivalent de l'arduino). Ce circuit se branche en USB au pc, et nous utiliserons quatre entrées digitale pour lire les quartes canaux du récepteur de votre télécommande. Le port USB fournit bien assez d'énergie pour alimenter votre récepteur de télécommande. Ceci est très pratique car vous n'avez donc pas a brancher quelque alimentation que ce soit sur votre récepteur.  
  
Une petite astuce pour assurer la connexion  entre le montage et le récepteur consiste à utiliser la connectique des boitiers de PC. En effet dans une tour de pc les boutons et les LEDs de façade se connectent à la carte mère et ces mêmes connecteurs sont parfaitement compatibles avec les pins de votre récepteur. Évidement si vous avez un boitier plastique autour de votre récepteur qui vous impose le détrompeur vous pouvez toujours limer les anges des connecteurs improvisés.


## Le programme informatique
  
Le programme pour arduino est très simple. Le framework arduino fournit une classe permettant d'utiliser le circuit en tant que joystick. Pour envoyer la position des axes du joystick à l'ordinateur on utilise l'objet Joystick qui comporte plusieurs setters X Y Z et Zrotate. Il suffit d'envoyer un entier compris entre 0 et 1023 représentant la position du joystick. Notez que le neutre correspond a la valeur 512.  
Pour lire les canaux du récepteur j'ai choisi de coder une classe nommée ServoRead. On créera un objet de cette classe par canal. Le contructeur de l'objet prend en paramètre le numéro de pin de l'arduino (teensy++ dans mon cas).  


### Fichier interfaceRC.ino  

```cpp
// Include des libs
#include "ServoRead.h"

ServoRead Sr1(38);
ServoRead Sr2(10);
ServoRead Sr3(20);
ServoRead Sr4(5);

int use_second_pulse = 1;

void setup() {
}

void loop() {

  int ch1, ch2, ch3, ch4;  
  long lastTime = millis();
  
  while ((millis() - lastTime) < 50) {
    ch1 = Sr1.checkPosition();
    ch2 = Sr2.checkPosition();
    ch3 = Sr3.checkPosition();  
    ch4 = Sr4.checkPosition();
  }
  
  if (use_seconde_pulse) {
    ch1 = Sr1.getPosition();
    ch2 = Sr2.getPosition();
    ch3 = Sr3.getPosition();  
    ch4 = Sr4.getPosition();  
  }
  
  Joystick.X(ch1);       
  Joystick.Y(ch2);       
  Joystick.Z(ch3);
  Joystick.Zrotate(ch4);
  
}
```
  
### Fichier ServoRead.h  

```cpp

/*
  Created by Artiom FEDOROV Juillet 2012
  Released into the public domain.
*/

#ifndef ServoRead_h
#define ServoRead_h

#include "Arduino.h"

class ServoRead
{
  public:
    ServoRead(int pin);
    long checkPosition(); 
    long getPosition();
        
  private:
    int _previousState;
    int _pin;
    long _lastTime;
    long _duration;
    long _position;
};

#endif
```
  
  
### Fichier ServoRead.cpp

```cpp
#include "Arduino.h"
#include "ServoRead.h"

ServoRead::ServoRead(int pin) {
    _pin = pin;
    pinMode(pin, INPUT);
    _previousState = digitalRead(pin);
    if (_previousState == LOW) {
      _lastTime = micros();
    } else {
      _lastTime = 0; 
    }
}


long ServoRead::checkPosition() {
    int pinState = digitalRead(_pin);
  
    if ((_previousState == LOW) && (pinState == HIGH)) {
       _lastTime = micros(); 
       _previousState = pinState;    
    }
  
    if ((_previousState == HIGH) && (pinState == LOW)) {
       _previousState = pinState;    
       _duration = micros() - _lastTime;
      _position = map(_duration, 1000, 2000, 0, 1023);   
    }
    return _position;
}


long ServoRead::getPosition() {
   return _position; 
}

```
  
  
## Utilisation côté ordinateur

![](fms.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Dans l'absolut le montage est complètement compatible avec tous les systèmes d'exploitation étant donné que l'arduino se comporte comme un joystick standard. De ce fait pour tester l'interface il vous suffit d'utiliser un petit logiciel de configuration de joystick sous linux tel que QJoyPad, sous windows la configuration du joystick peut se faire avec les outils proposés par défaut (dans les propriétés du périphérique). Une fois que l'on s'est assuré que l'interface est opérationnelle, on peut l'utiliser avec [FMS](http://fms.modelisme.com/) par exemple (excellent simulateur de vol de modèles réduits). Le joystick fonctionnera évidement avec tous les jeux ou logiciel supportant le joystick comme périphérique.  
  
  
  
  
## Quelques photos du projet en fonctionnement

{{% gallery %}}

![](P1010413.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010414.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010415.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010416.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010417.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010418.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010419.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010420.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010421.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010423.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}



  
## Quelques photos du projet

{{% gallery %}}

![](P1010400.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010401.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010402.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010403.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010404.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010405.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010406.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010409.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010410.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010412.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010424.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010425.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010426.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010428.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010429.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Documents annexes

[Télécharger les sources complètes du projet](http://artiom21.free.fr/projets/arduino-telecommande-rc-usb/interfaceRC.zip)