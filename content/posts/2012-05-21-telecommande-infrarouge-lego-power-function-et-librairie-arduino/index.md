---
date: '2012-05-21T14:05:20+02:00'
draft: false
title: "Télécommande infrarouge lego power function et librairie arduino"
slug: "telecommande-lego-power-functions-arduino"
tags:
  - arduino
  - electronique
  - informatique
  - lego
  - lego power functions
  - librairie arduino
  - telecommande lego
categories:
  - "Électronique"
cover:
  image: "telecommande-lego-et-recepteur.avif"
  alt: "Image d'illustration"
description: Découvrez comment contrôler le récepteur infrarouge LEGO Power Functions avec une carte Arduino/Teensy et la librairie LegoRC pour gérer la vitesse et le freinage.
showTOC: true
---

![](telecommande-lego-et-recepteur.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](telecommande-lego-et-power-functions.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Un chassis motorisé de légo technic est souvent très pratique pour réaliser une base pour un robot. L'idée de cet article est de vous présenter une librairie pour arduino qui permet de **commander le récepteur infrarouge des legos technics power functions**. Le principe de l'interface est d'émuler les signaux de la télécommande. En effet le protocole lego n'est pas très complexe, et surtout il ouvre la possibilité d'adresser le récépteur légo différemment et donc d'accéder  a de nouvelles fonctionnalités tels que la **vitesse de rotation** de chaque moteur (sur **7 niveaux**) et la **fonction de frein** qui permet d'immobiliser l'axe du moteur. Pour mettre en exemple cette librairie je vous propose de réaliser une télécommande améliorée pour lego technics power function.  


## Lego Power Functions récepteur

![](lego-power-functions.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Les légos power functions sont devenu assez courants dans des lots de taille considérable de lego technics. Les power functions se composent d'un moteur assez gros pour la motorisation généralement, d'un moteur de taille moyenne généralement pour contrôler des bras ou autres, d'un récepteur infrarouge d'un pack d'alimentation et de l'émetteur infrarouge. Chaque récepteur comporte deux connecteurs pour des moteurs et possède un switch pour régler le canal sur lequel il doit attendre les commandes. Chaque émetteur infrarouge comporte évidement la fonction de sélection de canal pour déterminer sur quel canal émettre.  


## Télécommande améliorée à base d'arduino
  
La télécommande que je vous présente ici est très simple. Son cout global n'excède pas une trentaine d'euros. En effet son composant principal est un teensy2.0++ qui est compatible à 100% avec l'IDE arduino.  
La télécommande comporte 8 boutons en tout. 4 boutons pour chaque moteur. Deux boutons servent a regler la vitesse et changer de sens pour chaque moteur. Un bouton permet d'envoyer un signal de vitesse nulle pour chaque moteur, et enfin un autre bouton permet d'envoyer la commande de frein pour chaque moteur. Cette commande permet d'appliquer une contrainte sur l'axe du moteur à l'arrêt.  

{{< youtube-lite "L0DfyOfxe7k" >}}


## Librairie pour arduino LegoRC

![](telecommande-et-recepteur-lego-pf.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Le code source permettant de communiquer avec le récepteur légo est une classe. Le constructeur de cette classe prend en paramètre la broche sur laquelle vous avez branché la diode infrarouge. On utilisera que trois méthodes publiques: sendCommand(int n1, int n2, int n3), sendSignalString(String msg), autoSend(). Chaque signal infrarouge se compose de 3 mots de 4 bits et d'un mot de vérification (checksum des 3 mots). SendCommand vous permet d'envoyer les 3 mots en entiers compris entre 0 et 15. La méthode sendSignalString, vous permet d'envoyer une chaine de caractères contenant les caractères '1' ou '0'. Cette chaine correspond a la concaténation des trois commandes en binaire. Cette chaine devra obligatoirement faire 16 caractères. Vous aurez donc dans ce cas là calculer la valeur du checksum vous mêmes.  


## Protocole infrarouge, signaux et documentation
  
Le protocole utilisé par le récepteur légo est expliqué en détail dans le document: [Lego Power Function RC v120.pdf](http://artiom21.free.fr/projets/arduino-lego-telecommande/LEGO%20Power%20Functions%20RC%20v120.pdf) . En effet dans ce document on comprends rapidement quels commande envoyer pour chaque comportement des moteurs voulus. J'attire votre attention sur le **Combo PWM mode**. Ce mode permet de contrôler les deux moteurs avec une seule commande envoyé. Pour envoyer les commandes au récepteur vous allez pouvoir utiliser la méthode sendCommand de la classe LegoRC. En effet les mots correspondent aux "nibble" de la documentation. Donc le premier mot sera un mot de configuration. Le deuxième la commande pour le moteur B et le troisième la commande pour le moteur A.  
Vous pouvez explorer ce document qui comporte tous les modes d'adressage supporté par le récepteur. J'ai choisi d'utiliser le Combo PWM mode car ce dernier permet d'avoir le contrôle de la vitesse. En effet chaque moteur a 7 niveaux de vitesse différente pour chaque sens.  
  
  
## Partie électronique de la télécommande

![](telecommande-lego-electronique.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

Comme dis ci dessus, la partie électronique ne présente vraiment aucune difficulté particulière. En effet tout le travail est assuré par le micro contrôleur Teensy2.0++. J'attire cependant votre attention sur quelques détails. Je vous recommande de ne pas oublier de mettre une résistance sur la led infrarouge. Résistance d'environ 220 Ohm. Par ailleurs pour bien distinguer chaque état des boutons il faut une résistance de rappel a la masse. Il s'agit de connecter la pin d'entrée de l'inter a la masse à travers d'une résistance d'environ 30 kOhm. et le bouton positionnera cette pin au +5V lorsque le bouton est enfoncé. Par ailleurs le ciruit est entièrement auto alimenté par l'USB du teensy. Il ne faudra donc surtout pas oublier de relier les broches GND et +5V du teensy à celles du circuit.  


## Quelques photos

{{% gallery %}}

![](P1010057.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010058.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010059.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010060.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010063.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010064.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010065.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010066.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010067.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010068.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Documents annexes
  
- [Lego Power Function RC v120.pdf](http://artiom21.free.fr/projets/arduino-lego-telecommande/LEGO%20Power%20Functions%20RC%20v120.pdf)  
- [Classe LegoRC pour arduino.zip](http://artiom21.free.fr/projets/arduino-lego-telecommande/Classe%20LegoRC%20pour%20arduino.zip)  
- [Programme complet telecommande infrarouge lego pour arduino.zip](http://artiom21.free.fr/projets/arduino-lego-telecommande/Programme%20complet%20telecommande%20infrarouge%20lego%20pour%20arduino.zip)
