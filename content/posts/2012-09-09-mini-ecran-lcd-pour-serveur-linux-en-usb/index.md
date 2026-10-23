---
date: '2012-09-09T14:05:20+02:00'
draft: false
title: "Interface télécommande RC en Joystick USB"
slug: "mini-ecran-lcd-en-usb"
tags:
  - arduino
  - electronique
  - informatique
  - linux
  - teensy
  - usb
categories:
  - Électronique
cover:
  image: "P1010484.avif"
  alt: "Image d'illustration"
  hiddenInSingle: true
description: Découvrez comment fabriquer un mini écran LCD USB avec un Teensy ou Arduino pour suivre vos scripts et processus Linux en temps réel depuis votre serveur.
showTOC: true
---


![Ecran lcd arduino en usb](P1010484.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![Ecran lcd teensy2](P1010483.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Le **mini écran** pour serveur est un petit projet très simple mais potentiellement extrêmement utile. Lorsque vous travaillez dans l'informatique vous êtes souvent amenés a utiliser des scripts (**perl**, **php**, etc) divers et variés qui tournent et qui effectuent à votre place des tâches répétitives. Il est alors intéressant de pouvoir suivre l'évolution de ces scripts en temps réel pour savoir si ce dernier tourne toujours où il en est dans le traitement. La solution simple consiste a utiliser son moniteur mais avec le projet mini LCD en USB vous pourrez très simplement **envoyer vos message de script directement sur un petit ecran LCD branché en USB**. De ce fait vous pourrez même éteindre l'écran principal de votre machine tout en **gardant un oeuil sur les processus en cours** dans votre machine.

## Le montage électronique
  
Le montage électronique est très simple. Tout tourne autour d'un micro contrôleur Teensy++ (équivalent de l'Arduino). Vous pouvez brancher les pins de l'écran sur n'importe quels entrées/sorties du teensy, c'est le soft qui sera adapté au brochage électronique choisi. Vous pouvez tout à fait vous inspirer de la documentation arduino sur les écrans LCD: [ardiuno liquid crystal](http://arduino.cc/en/Tutorial/LiquidCrystal). Etant donné mes contraintes purement physiques d'emplacement des ports j'ai choisi le brochage comme expliqué sur le schémas électronique ci dessous. Les seuls composants facultatifs sur le schémas sont le potentiommetre permettant de régler la luminausite de l'écran (ce dernier peut facilement être remplacé par la bonne valeur de la résistance pour correspondre a une luminausité satisfaisante pour vous), la LED rouge signalant les moments ou le circuit lit le port USB, et la LED verte signalant que le circuit est bien sous tension.
  
![Schema electronique de brochage lcd sur arduino](MiniLCDenUSB.avif)
{ .article-image-right mode="lightbox" }
  

## Le programme informatique du mini moniteur en USB

Le programme informatique va lire tout simplement le port USB en tant que périphérique série. Tous les caractères lus sont traduits ensuite a l'écran tel quel. Remarquez que c'est dans la boucle de récéption usb: while(Serial.available()) que j'active la diode éléctroluminescente rouge, cela permet de savoir rapidement si le circuit est en réception de message ou pas. Par ailleurs le montage permet d'avoir un historique sur 2 lignes. En effet les messages envoyés consécutivement vont se décaler de ligne en ligne. La dernière ligne correspondant au dernier message envoyé sur l'USB  
  
```cpp
#include <liquidcrystal.h>

LiquidCrystal lcd(24, 25, 8, 9, 27, 0);
int led = 12;
String l1="", l2="", tmpl="";
char incomingByte;
int newMSG = 0;


void setup() {
  pinMode(led, OUTPUT);
  lcd.begin(16, 2);
  Serial.begin(9600);
  
}

void loop() {
  
  while (Serial.available()) {
    digitalWrite(led, HIGH);      // indicateur de reception data USB
    incomingByte = Serial.read();
    tmpl = tmpl + char(incomingByte);
    newMSG = 1;
  }

    digitalWrite(led, LOW);  

    if (newMSG) {
      l1 = l2;
      l2 = tmpl.trim();
      
      lcd.clear();
      
      lcd.setCursor(0, 0);
      lcd.print(String(l1));      

      lcd.setCursor(0, 1);
      lcd.print(String(l2));      
      tmpl = "";      
    }
    
    newMSG = 0;
}
```


## Fonctionnement côté console
  
Pour envoyer une chaine de caractère depuis la **console Linux**, il vous suffit de taper la commande suivate:  
 
```bash
echo "Message test">/dev/ttyACM0
```


La partie "Message test" peut être remplacé par ce dont vous avez besoin. Vous pouvez du coup utiliser l'écran LCD en USB depuis **n'importe quel language** supportant la possibilité d'exécuter des commandes dans la console.  
  
Par exemple en **PHP** vous pouvez ecrire  
  
```php
exec('echo "Message test">/dev/ttyACM0');
```
  
Ou alors en **C/C++** vous pouvez faire  
  
```cpp
system("echo \"Message test\" > /dev/ttyACM0"); 
```
  

## Photos du projet mini ecran LCD en USB pour serveur

{{% gallery %}}

![](P1010479.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010480.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010481.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010482.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010483.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010484.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010485.avif)
{ mode="lightbox" miniature-width=200 }

![Envoyer commandes depuis le shell vers USB](P1010486.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}
