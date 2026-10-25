---
date: '2012-05-02T14:05:20+02:00'
draft: false
title: Programmateur de 16F84 avec un Teensy++ (Arduino)
slug: programmateur-16F84-avec-arduino
tags:
  - 16f84
  - arduino
  - electronique
  - informatique
  - programmateur 16f84
  - teensy
categories:
  - Électronique
cover:
  image: https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCP4SfaD3JclJ8Kjez6Jjt6RDC089C63z4b6A6w46fNmDV9_FXyJ033zu5xw66zWZkuO-vQntSV8tiKDj0twRY2O7Xrqdx523b3fGl1GISwuBC938GiGKXFm9BQ2JSy0YaOb_wdsdqD9o/s1600/PICT0006.JPG
  alt: "Image d'illustration"
description: 
showTOC: true
---


### Programmateur de 16F84 avec un Teensy++ (Arduino)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCP4SfaD3JclJ8Kjez6Jjt6RDC089C63z4b6A6w46fNmDV9_FXyJ033zu5xw66zWZkuO-vQntSV8tiKDj0twRY2O7Xrqdx523b3fGl1GISwuBC938GiGKXFm9BQ2JSy0YaOb_wdsdqD9o/s1600/PICT0006.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCP4SfaD3JclJ8Kjez6Jjt6RDC089C63z4b6A6w46fNmDV9_FXyJ033zu5xw66zWZkuO-vQntSV8tiKDj0twRY2O7Xrqdx523b3fGl1GISwuBC938GiGKXFm9BQ2JSy0YaOb_wdsdqD9o/s1600/PICT0006.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNRzE7yLa5NxxWCJ6oCBonWTXNCA6Dn7dnZSa7j-kTRwKJf2gFtRKMYgkcVsiYox8YIV4smF-L_ZwFXfsJ8RZ3g7HyNZNT1bcvclHNZEFk1qkQ1eXhyr3RbnTNHmXQEGgo4cSDuCyNsII/s1600/PICT0011.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNRzE7yLa5NxxWCJ6oCBonWTXNCA6Dn7dnZSa7j-kTRwKJf2gFtRKMYgkcVsiYox8YIV4smF-L_ZwFXfsJ8RZ3g7HyNZNT1bcvclHNZEFk1qkQ1eXhyr3RbnTNHmXQEGgo4cSDuCyNsII/s1600/PICT0011.JPG)Ayant pas mal travaillé avec le **16F84** par le passé j'ai voulu proposer une **lib pour arduino** afin de permettre de **programmer un 16F84** avec un **Teensy2++** (équivalent de la platine Arduino).  
  
Le fonctionnement de la lib est très simple. Pour programmer un 16F84 avec l'arduino, il vous suffira d'inclure la lib dans votre projet, declarer l'**objet Pic16F84**, déclarer une variable String contenant le programme en hexadécimal puis lancer la methode correspondant à l'**envoi du programme dans le 16F84**.  
  

  

|   |
|---|
|[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh_AMHWD3sxN7UkXkGd82Wp9PkSPLXjg_RwUguG-UXiICuDvSeYe78Tz_QDOA2TEY0EjT4rcd3N2lX0Hv9nQm5v-wjBBBjEb6_DSONJtl5QolcRZv_bA0Jz756vnD18wYW_aByPRok7nWc/s320/Programmateur-16F84-Teensy-arduino.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh_AMHWD3sxN7UkXkGd82Wp9PkSPLXjg_RwUguG-UXiICuDvSeYe78Tz_QDOA2TEY0EjT4rcd3N2lX0Hv9nQm5v-wjBBBjEb6_DSONJtl5QolcRZv_bA0Jz756vnD18wYW_aByPRok7nWc/s1600/Programmateur-16F84-Teensy-arduino.jpg)|
|Programmateur de 16F84 avec un teensy2++|

**Microcontroleur 16F84**  
Le 16F84 est un microcontroleur relativement simple a prendre en main et très répandu dans le domaine de l'électronique. En effet généralement cadencé a 4Mhz avec 12 ports entés/sorties il offre pas mal de possibilités dans la robotique ou dans les automates en général pour un cout plus que raisonnable.  
  
**Teensy++ arduino**  
Aujourd'hui avec la baisse des couts dans l'électronique des circuits plus performants et surtout plus simples a mettre en oeuvre sont privilégiés. C'est le cas du teensy2++. En effet le teensy se programme soit en C soit avec l'IDE de l'arduino avec laquelle il est 100% compatible. Le teensy propose une quarantaine de ports entrées sorties dont pas mal d'analogiques. Ces caractéristiques et son faible cout le rendent très performant et accessible au plus grand nombre. Le programmateur est directement intégré et se connecte par le biais du port USB au pc pour le transfert des programmes  
  
L'idée générale du projet est d'offrir la possibilité de reprogrammer un circuit 16F84 avec un Teensy (arduino) en cours d'exécution. Cela permettrait par exemple de se servir du 16F84 comme périphérique pouvant être spécialisée en cours d'exécution du teensy. Par exemple dans le cas de la robotique on pourrait tout a fait imaginer que le 16F84 sert de contrôleur de servo moteurs et l'arduino envoi juste les positions pour chaque servo moteur en I2C par exemple.  
  
**Comment utiliser la lib de programmation du 16F84 avec un Arduino**  
  
La lib est très simple a utiliser. Tout d'abord vous devez télécharger les fichiers Pic16F84.cpp et Pic16F84.h.  
  
vous pouvez les télécharger depuis le dépot svn:  
  
[https://arduino-16f84-programer.googlecode.com/svn/trunk/](https://arduino-16f84-programer.googlecode.com/svn/trunk/)  
  
Vous pouvez copier ces fichier dans votre projet puis les intégrer au projet en incluant le fichier Pic16f84.h  

#include "Pic16F84.h"

  
Ensuite vous devez créer l'objet Pic16F84. Le constructeur de la classe prend en parametre les pins que vous avez utilisé pour connecter votre 16F84  

Pic16F84(int pinVmax, int pinReset, int pinClock, int pinData);

  
pinVmax: correspond au controle du +12V a la broche 4 du 16F84 soit le MCLR.  
pinReset: correspond au reset du circuit. quand envoie 1 alors mettre la broche 4 a la masse  
pinClock: correspond au signal d'horloge. Broche 12 RB6 sur le pic 16F84  
pinData: correspond a la donnée. Broche 13 RB7 sur le pic 16f84.  
  
Donc la déclaration peut se faire de la manière suivante:  

// Brochage 16F84
Pic16F84 pic(45, 44, 42, 43);

  
Ensuite pour communiquer avec 16F84 vous avez les méthodes suivantes:  

pic.eraseChip();
pic.loadProgram(programm);
pic.loadConfiguration(confWord);

  
Le loadConfiguration permet d'envoyer la valeur de la mémoire de configuration du 16F84. C'est une valeur hexa comprise entre 0000 et 3FFF.  
  
**Particularités de la lib et du fichier .hex**  
  
Le fichier hexadécimal se présente sous la forme suivante:  
  
:100000000428FF3FFF3FFF3F031383128C0185014C  
:10001000831685018601831286010C09C000400801  
:100020008C0040080319162886151728861182307F  
:10003000CB00FF30CA00CB0B1E282128CA0B1E287C  
:100040001B288730CA00CA0B232800000D28272848  
:02400E00FA3F77  
:00000001FF  
  
Ce code permet de faire clignoter une diode branché sur le port RB3 du 16F84 soit la broche 9.  
  
Ce fichier contient pas mal de choses qui ne vont pas nous intéresser. Pour commencer les 8 premiers caractères représentent l'emplacement adresse. Les deux derniers caractères représentent le checksum de la ligne. Donc ne nous intéressent pas non plus. Vous devez donc formater votre programme afin que votre code source ressemble a ce qui suit:  
  
0428FF3FFF3FFF3F031383128C018501  
831685018601831286010C09C0004008  
8C004008031916288615172886118230  
CB00FF30CA00CB0B1E282128CA0B1E28  
1B288730CA00CA0B232800000D282728  
  
L'avant derniere ligne du programme original est le config word. adresse :02400E00. Pour isoler la valeur de config on supprime les 8 premiers carracteres de la ligne correspondante, puis les deux dernièrs carractères. On se retrouve donc avec le config word: FA3F.  
  
Attention!!! Tous les codes héxa dans le fichier hexadecimal sont inversés par rapport aux vrais valeurs envoyés. C'est a dire si on prend le premier mot du programme on voit 0428, en réalité le code correspondant est 2804. La lib corrige cette spécificité pour le programme. Par contre pour le config word vous devez envoyer le bon directement. Donc non pas FA3F mais 3FFA.  
  
**Un exemple d'utilisation de la lib**  
  
Considérons le brochage électronique suivant:  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgG4l_nnnwUQ-F4XEmeT9oFBrpceRJMIu575EhjYWYOQgqFmh1CO24U4pN30szyGFfnOPqsGmmzwFwsH9rGI8YowXl9P6b-VHubV3idbZ4idGRB3qtXIetk8Qnco5GX3n2t5eiExMBbLjk/s640/Programmateur+16f84+arduino+teensy.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgG4l_nnnwUQ-F4XEmeT9oFBrpceRJMIu575EhjYWYOQgqFmh1CO24U4pN30szyGFfnOPqsGmmzwFwsH9rGI8YowXl9P6b-VHubV3idbZ4idGRB3qtXIetk8Qnco5GX3n2t5eiExMBbLjk/s1600/Programmateur+16f84+arduino+teensy.png)

  
Voici un exemple de programme simpliste qui fonctionnera avec ce brochage:  
  

// include the library code:
#include "Pic16F84.h"
String programm = "0428FF3FFF3FFF3F031383128C018501831685018601831286010C09C00040088C004008031916288615172886118230CB00FF30CA00CB0B1E282128CA0B1E281B288730CA00CA0B232800000D282728";
String confWord = "3FFA";

// Brochage 16F84
Pic16F84 pic(45, 44, 42, 43);

void setup() {
   pic.eraseChip();
   pic.loadProgram(programm);
   pic.loadConfiguration(confWord);
}

void loop() {
  
}

  
  
  
**Vidéo du montage en fonctionnement**  
  
   
  
  
**Documents annexe**  
  
[Microchip ISCP Guide 16F84](http://artiom21.free.fr/projets/arduino-16F84-programer/30277d%20-%20ISCP%20Guide%2016f84.pdf)  
[Microchip Datasheet 16F84](http://artiom21.free.fr/projets/arduino-16F84-programer/Datasheet%2016F84.pdf)  
[Site source du programme hexa blinking led 16F84](http://www.best-microcontroller-projects.com/pic16f84.html)  
  
  
  
  