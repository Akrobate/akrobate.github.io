---
date: '2016-11-03T14:05:20+02:00'
draft: false
title: Programmateur de atmega328 avec un teensy 2++
slug: programmateur-atmega328-avec-un-teensy
tags:
  - arduino
  - informatique
  - teensy
  - atmega328p
categories:
  - électronique
cover:
  image: "20170619_213403.avif"
  alt: "Logo du projet weather tracker"
description: "Apprenez à programmer un microcontrôleur ATmega328 vierge et à installer le bootloader Arduino à l'aide d'une carte Teensy 2++. Guide pas à pas et schémas !"
showTOC: true
---

![](20170619_212603.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](20170619_213403.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }


Dans cet article nous allons voir comment réaliser un programmateur de microcontrôleur atmega328 avec le Bootloader de l'Arduino. Pourquoi spécifiquement ce microcontrôleur là ? Simplement parce que ce dernier équipe le très répandu Arduino UNO. L'objectif premier étant de s'affranchir de la grosse carte que représente l'arduino Uno pour ne garder que l'essentiel (a savoir le microcontrôleur en boîtier dip 28 ainsi que quelques composants classiques) et pouvoir disposer à peu de choses près des mêmes fonctionnalités. Donc ici nous allons partir du principe que votre atmega328 vous a été livré vierge de toute programmation (pas de bootloader). Pour cette raison en premier lieu nous verrons comment charger le bootloader (compatible Arduino IDE), puis en deuxième lieu comment charger vos programmer dans la mémoire du contrôleur et enfin nous réaliserons un petit chenillard avec notre « Arduino Uno » fraîchement programmé !


## Petit tour rapide du ATmega328

Je ne m'attarderais pas trop sur ce sujet car il existe une multitude de documentations sur le net et les familiers du Arduino Uno savent déjà ce que l'on peut faire avec.

Cependant quelques rappels de base sur le microcontrôleur peuvent être bien pratiques :

- 20 entrées / sorties
- 6 entrées analogiques parmi les 20 entrées / sorties
- 6 sorties PWM (parmi les 20)
- Fréquence jusqu'à 20Mhz
- Alimentation nominale 5V


## Chargement du bootloader dans le atmega328 via un Teensy 2 ++

Le bootloader est un petit programme qui pilote le microcontrôleur à très bas niveau. En effet ce programme se charge généralement une seule fois dans le circuit et permet de définir la séquence de boot, le comportement de la puce lors de l'introduction d'un nouveau programme et autres fonctionnalités bas niveau. Par exemple dans le cas de ATMega328 une des fonctionnalités du bootloader est de rendre disponible l'upload de programmes via le port série standard (pins TX/RX) du microcontrôleur. En gros cela fait pas mal penser au bios d'un ordinateur qui justement sert à définir entre autres choses la séquence de boot et l'initialisation du hardware.

Commençons par la partie électronique. Branchez le Teensy à votre Atmel atmega328

Suivez la connectique comme indiqué sur le schémas.

![](bootloader-electronic-schema.avif)
{ mode="lightbox" }

A présent préparons notre Teensy afin que ce dernier puisse envoyer le bootloader au atmega328. Pour ce faire réalisez simplement les étapes suivantes :

- Ouvrez votre IDE Arduino, selectionez Teensy 2++ comme board de destination dans le menu Outils.
    
- Ouvrez dans les exemples ArduinoISP et sauvegardez le projet localement car nous allons modifier quelques lignes de code pour que le du programme suive bien la connectique du schéma.
    
    - Recherchez la ligne « #define LED_HB 9 » et remplacez le numéro de la PIN 9 en 6 ce qui donnerait « #define LED_HB 6 ». La constante LED_HB sert à définir la broche sur laquelle est branché la LED du « heart beat » qui est un indicateur de disponibilité du programmateur. En gros cela va nous permettre de constater visuellement via le clignotement de la diode que le programmateur est prêt à envoyer des donnés. On change la valeur en 6 car c'est là que se trouve branchée la diode sur la carte du teensy 2 ++.
        
    - Recherchez la ligne « #define RESET 10 » et changez le 10 en 20. En effet sur le schema électronique nous avons branché le RESET du atmega328 sur la pin 20 du Teensy.
        
- Compilez et chargez le programme dans votre Teensy.
    
- Vérifiez que la diode sur le Teensy s'est mise a clignoter. C'est le heart beat. Si cela clignote vous êtes prêts a charger le bootloader. Dans le cas contraire assurez vous que vous avez bien changé la valeur de la constante LED_HB


Maintenant que votre teensy est prêt effectuez les étapes suivantes pour charger le bootloader dans notre microcontrôleur.


- Dans l'IDE Arduino sélectionnez à présent le atmega328 comme microcontrôleur. Pour ce faire allez dans _Outils_ > _Board_ > _Arduino Duemilanove or Diecimila_. Assurez vous que quand vous cliquez sur le menu _Outils > Processeurs > ATmega328_ est sélectionné.
    
- Définissez le programmateur dans _Outils > Programmateur > Arduino as ISP_
- Assurez vous que votre Teensy est bien reconnu par l'IDE Arduino dans Outils > port > `/dev/ttyACM0`
- Et enfin cliquez sur Outils > **Graver la séquence d'initialisation**
    
L'opération semblerait-t-il peut prendre un certain temps (jusqu'à une minute). Dans mon cas ce fut quasi instantané. Une fois chargé, vous aurez un message dans la console vous confirmant le succès du chargement du bootloader dans le microcontrôleur.

  
Si vous rencontrez un log (message dans la conseole) qui vous dit quelque chose comme :

avrdude: _Device signature_ = 0x000000 avrdude: _Expected signature_ for _ATMEGA328P_ is 1E 95 0F

Vérifiez votre brochage, vérifiez que la pin du RESET est bien mappé sur le bon port dans le code.

Voilà votre Arduino UNO fait maison est prêt ! Vous n'avez plus a refaire cette opération. A présent votre at328 se comporte comme l'Arduino UNO, et va pouvoir être programmé via son port série. C'est ce que nous verrons dans la prochaine section.


## Chargement d'un programme via TX/RX dans le ATmega328

Tout comme pour la phase du chargement, nous aurons besoin de préparer un peu notre Teensy afin que ce dernier se comporte comme une simple interface USB vers série. Pour ce faire vous invite a récuperer le code depuis mon github:  
  
[https://github.com/Akrobate/ArduinoSerialProgrammer](https://www.blogger.com/blog/post/edit/294242587156974763/1620452871133516405#)  
  
Une fois que vous avez récuperé le code chargez le programme dans le Teensy.  

A l'origine le code source provient de cet excellent article:

[https://dorkbotpdx.org/blog/paul/teensy_as_benito_at_57600_baud](https://www.blogger.com/blog/post/edit/294242587156974763/1620452871133516405#)

  
  
## Mapping et partie éléctronique
  

Ici tout comme pour la première partie nous pouvons adapter le mapping
  
Reset pin est cablé sur la pin 4 du teensy, mais vous pouvez changer ca, ca n'impacte pas le fonctionnement du programmateur.  
  

La constante led_pin est cablé en pin 6 (Une fois de plus cela correspond a la led sur le Teensy2++).

  

Le schémas électronique est très simple, il consiste simplement à brancher le port TX/RX aux port TX/RX du ATmega328.  
  
Juste au cas où vous auriez un doute, la pin TX du Teensy doit aller sur la pin RX du ATMega328, et réciproquement la pin RX du Teensy doit aller sur la pin TX du ATMega.
  
![](programmer-electronic-schema.avif)
{ mode="lightbox" }
  

Une fois les branchements faits, la procédure pour charger un programme est très simple (beaucoup d'étapes sont déjà bien configurées si vous avez chargé le bootloader juste avant)  
  
Revenons a notre Arduino IDE et faisons les étapes suivantes:

- Ouvrez le programme que vous souhaitez uploader dans le ATmega328
    
- Outils > Board > Arduino Duemilanove or Diecimila
    
- Outils > Processeurs > ATmega328
    
- Outils > Programmateur > Arduino as ISP
    
- Outils > port > **/dev/ttyACM0**


Vous voilà prêts à envoyer votre programme. Vérifiez le code et Téléversez.  


## Schémas de test 8 LEDS pour jouer avec le microcontroleur ATmega328

Voici une petite suggestion de cablage de test pour le ATmega328. Ce petit chenillard montage utilise que les ports restants et donc non occupé par le brochage du bootloader ou du programme. En gros cela va vous permettre de faire des tests in-situ, c'est à dire que vous n'aurez aucune étape de branchement entre l'upload du programme et le test du code du ATmega328.

  
![](demo-Atmega328p-electronic-schema.avif)
{ mode="lightbox" }

En effet tout au long des 3 schémas j'ai veillé a ce que toutes les pins utilisées soient différentes, ce qui fait que vous pouvez câbler des le début les 3 schémas, puis juste jouer avec le software pour passer d'une étape à l'autre.  
  
## Sources de l'article et liens utiles

- [http://dnrce.com/articles/using-a-teensy-to-program-a-breadboard-arduino](https://www.blogger.com/blog/post/edit/294242587156974763/1620452871133516405#)
  
- [https://dorkbotpdx.org/blog/paul/teensy_as_benito_at_57600_baud](https://www.blogger.com/blog/post/edit/294242587156974763/1620452871133516405#)  
  
- [https://github.com/Akrobate/ArduinoSerialProgrammer](https://www.blogger.com/blog/post/edit/294242587156974763/1620452871133516405#)