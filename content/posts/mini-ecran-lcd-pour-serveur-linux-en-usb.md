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
  image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4Ka9T0QYlCSeTm5A_7CDxsN9kCV31AmO2IivK44OBK7VIu5zvl2O6MSxBZdLdfx05QFThp_O7k8O8JJRQuNUAt44n2D7axEKp87lGijXsumnrAqzP2ctFPNaEK1RHhP5D19uwvVwMRE/s1600/P1010484.JPG"
  alt: "Image d'illustration"
---


### Mini écran LCD pour serveur (linux) en USB

[![Ecran lcd arduino en usb](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4Ka9T0QYlCSeTm5A_7CDxsN9kCV31AmO2IivK44OBK7VIu5zvl2O6MSxBZdLdfx05QFThp_O7k8O8JJRQuNUAt44n2D7axEKp87lGijXsumnrAqzP2ctFPNaEK1RHhP5D19uwvVwMRE/s200/P1010484.JPG "Ecran lcd arduino en usb")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4Ka9T0QYlCSeTm5A_7CDxsN9kCV31AmO2IivK44OBK7VIu5zvl2O6MSxBZdLdfx05QFThp_O7k8O8JJRQuNUAt44n2D7axEKp87lGijXsumnrAqzP2ctFPNaEK1RHhP5D19uwvVwMRE/s1600/P1010484.JPG)[![Ecran lcd teensy2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuhd4SGV2IVEL9kHXjp-RA97kAMvsM11UDmCl89ytRfUGYjggNUeFq8FMBmwBnUs_cXNY3ysSkyNKBE_IcfidKbrE3HzogTkNp8vNjcqtx26lP4rbk8eAG0gHvBXQW9FgrKFM3BOqIal4/s200/P1010483.JPG "Ecran lcd avec larduino")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuhd4SGV2IVEL9kHXjp-RA97kAMvsM11UDmCl89ytRfUGYjggNUeFq8FMBmwBnUs_cXNY3ysSkyNKBE_IcfidKbrE3HzogTkNp8vNjcqtx26lP4rbk8eAG0gHvBXQW9FgrKFM3BOqIal4/s1600/P1010483.JPG)Le **mini écran** pour serveur est un petit projet très simple mais potentiellement extrêmement utile. Lorsque vous travaillez dans l'informatique vous êtes souvent amenés a utiliser des scripts (**perl**, **php**, etc) divers et variés qui tournent et qui effectuent à votre place des tâches répétitives. Il est alors intéressant de pouvoir suivre l'évolution de ces scripts en temps réel pour savoir si ce dernier tourne toujours où il en est dans le traitement. La solution simple consiste a utiliser son moniteur mais avec le projet mini LCD en USB vous pourrez très simplement **envoyer vos message de script directement sur un petit ecran LCD branché en USB**. De ce fait vous pourrez même éteindre l'écran principal de votre machine tout en **gardant un oeuil sur les processus en cours** dans votre machine.

  
  
  
  
**Le montage électronique**  
  
Le montage électronique est très simple. Tout tourne autour d'un micro contrôleur Teensy++ (équivalent de l'Arduino). Vous pouvez brancher les pins de l'écran sur n'importe quels entrées/sorties du teensy, c'est le soft qui sera adapté au brochage électronique choisi. Vous pouvez tout à fait vous inspirer de la documentation arduino sur les écrans LCD: [ardiuno liquid crystal](http://arduino.cc/en/Tutorial/LiquidCrystal). Etant donné mes contraintes purement physiques d'emplacement des ports j'ai choisi le brochage comme expliqué sur le schémas électronique ci dessous. Les seuls composants facultatifs sur le schémas sont le potentiommetre permettant de régler la luminausite de l'écran (ce dernier peut facilement être remplacé par la bonne valeur de la résistance pour correspondre a une luminausité satisfaisante pour vous), la LED rouge signalant les moments ou le circuit lit le port USB, et la LED verte signalant que le circuit est bien sous tension.  
  
  

 [![Schema electronique de brochage moniteur sur teensy](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMNuZ2J428DzRSYNxgMADQtRNBaZdhXj2mz34i5Z-ChBWrudj4HPuXyMWRitoBCwzzN7MRTEF2tbXU9QQDGKFJKyv7I9Pg6MKxUsL_Ubl-zS3HlejSkkPhR_AUyaPw5PmFMqVcqxs1P7U/s640/MiniLCDenUSB.png "Schema electronique de brochage lcd sur arduino")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMNuZ2J428DzRSYNxgMADQtRNBaZdhXj2mz34i5Z-ChBWrudj4HPuXyMWRitoBCwzzN7MRTEF2tbXU9QQDGKFJKyv7I9Pg6MKxUsL_Ubl-zS3HlejSkkPhR_AUyaPw5PmFMqVcqxs1P7U/s1600/MiniLCDenUSB.png)

  

  

**Le programme informatique du mini moniteur en USB**

  
Le programme informatique va lire tout simplement le port USB en tant que périphérique série. Tous les caractères lus sont traduits ensuite a l'écran tel quel. Remarquez que c'est dans la boucle de récéption usb: while(Serial.available()) que j'active la diode éléctroluminescente rouge, cela permet de savoir rapidement si le circuit est en réception de message ou pas. Par ailleurs le montage permet d'avoir un historique sur 2 lignes. En effet les messages envoyés consécutivement vont se décaler de ligne en ligne. La dernière ligne correspondant au dernier message envoyé sur l'USB  
  
  

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

  
  
  
**Fonctionnement côté console**  
  
Pour envoyer une chaine de caractère depuis la **console Linux**, il vous suffit de taper la commande suivate:  
  

echo "Message test">/dev/ttyACM0

  
  
La partie "Message test" peut être remplacé par ce dont vous avez besoin. Vous pouvez du coup utiliser l'écran LCD en USB depuis **n'importe quel language** supportant la possibilité d'exécuter des commandes dans la console.  
  
Par exemple en **PHP** vous pouvez ecrire  
  

exec('echo "Message test">/dev/ttyACM0');

  
Ou alors en **C/C++** vous pouvez faire  
  

system("echo \"Message test\" > /dev/ttyACM0"); 

  
  
**Photos du projet mini ecran LCD en USB pour serveur**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg-p9xN7wuLpCdW2XX7O5W3I9WfsV1btZNldISidXqzLkQJh_Gola2U7rNy8Kuq6Vd8DA9Rb_suzht187SQdfmy7VopQLeAggXdwP2Kfm2H7R_yEsFpyofXVA0Mx4RbeCi63k2EgT97cg4/s200/P1010479.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg-p9xN7wuLpCdW2XX7O5W3I9WfsV1btZNldISidXqzLkQJh_Gola2U7rNy8Kuq6Vd8DA9Rb_suzht187SQdfmy7VopQLeAggXdwP2Kfm2H7R_yEsFpyofXVA0Mx4RbeCi63k2EgT97cg4/s1600/P1010479.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiLJkM6ZMDpmlMpPHlZ0eVd-1fOHZADs0NU1urgWcrrDPAEnzgpi61g_5XNv8OkU2RwHMhDvSCPXgwrxFBHQvfyq82hwILxtanpq97FTjs5mJCI0_REfjvqEdgtQUWffQwcrGT_HxEEPTo/s200/P1010480.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiLJkM6ZMDpmlMpPHlZ0eVd-1fOHZADs0NU1urgWcrrDPAEnzgpi61g_5XNv8OkU2RwHMhDvSCPXgwrxFBHQvfyq82hwILxtanpq97FTjs5mJCI0_REfjvqEdgtQUWffQwcrGT_HxEEPTo/s1600/P1010480.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidHgJq0ztAaZj9VkHiqTccteV9c505e4uRS1Xdo96BOQiazO2pjNEag6IbwjOAtkVEF9wmvySF1wrJGJeOksmNz_6FZCzXaNC56Mi8sbPsvRzo_kqHbUgMfo5RjVYh8mkKVFO4dB6N2a4/s200/P1010481.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidHgJq0ztAaZj9VkHiqTccteV9c505e4uRS1Xdo96BOQiazO2pjNEag6IbwjOAtkVEF9wmvySF1wrJGJeOksmNz_6FZCzXaNC56Mi8sbPsvRzo_kqHbUgMfo5RjVYh8mkKVFO4dB6N2a4/s1600/P1010481.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjF3B6pE64FTD1XZMugQfZGPZEWlnmR8idQ9QqVrqN5ERBhxmfaMJV74mmGvCpOOi2WxhG5itrimLF5mV36wnFHPfxxt4tprW9gQEovocDait4WxpSkYxU9W8InzLfLCbE-XFkDjXg6ua0/s200/P1010482.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjF3B6pE64FTD1XZMugQfZGPZEWlnmR8idQ9QqVrqN5ERBhxmfaMJV74mmGvCpOOi2WxhG5itrimLF5mV36wnFHPfxxt4tprW9gQEovocDait4WxpSkYxU9W8InzLfLCbE-XFkDjXg6ua0/s1600/P1010482.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuhd4SGV2IVEL9kHXjp-RA97kAMvsM11UDmCl89ytRfUGYjggNUeFq8FMBmwBnUs_cXNY3ysSkyNKBE_IcfidKbrE3HzogTkNp8vNjcqtx26lP4rbk8eAG0gHvBXQW9FgrKFM3BOqIal4/s200/P1010483.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjuhd4SGV2IVEL9kHXjp-RA97kAMvsM11UDmCl89ytRfUGYjggNUeFq8FMBmwBnUs_cXNY3ysSkyNKBE_IcfidKbrE3HzogTkNp8vNjcqtx26lP4rbk8eAG0gHvBXQW9FgrKFM3BOqIal4/s1600/P1010483.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4Ka9T0QYlCSeTm5A_7CDxsN9kCV31AmO2IivK44OBK7VIu5zvl2O6MSxBZdLdfx05QFThp_O7k8O8JJRQuNUAt44n2D7axEKp87lGijXsumnrAqzP2ctFPNaEK1RHhP5D19uwvVwMRE/s200/P1010484.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4Ka9T0QYlCSeTm5A_7CDxsN9kCV31AmO2IivK44OBK7VIu5zvl2O6MSxBZdLdfx05QFThp_O7k8O8JJRQuNUAt44n2D7axEKp87lGijXsumnrAqzP2ctFPNaEK1RHhP5D19uwvVwMRE/s1600/P1010484.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4slpJPztwBXeDw6bXwhPA6MKD5ga0TTtZ12gzngMG8ei3nXWwZH_8fgJTG5btJEkeWmrx-MfDo3BitT9i3NrFdaPdeZ2OrFsFAuN_zeovFkHJqX_OE09wUIHMiAoQmIK2SAo8uoUXv1M/s200/P1010485.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4slpJPztwBXeDw6bXwhPA6MKD5ga0TTtZ12gzngMG8ei3nXWwZH_8fgJTG5btJEkeWmrx-MfDo3BitT9i3NrFdaPdeZ2OrFsFAuN_zeovFkHJqX_OE09wUIHMiAoQmIK2SAo8uoUXv1M/s1600/P1010485.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiNwQdsO3w5IA68bjygu48chvMB5pk5R0lOl1XbbJgXoEVBH3Fs3YE3BEBjVdhd6Wr0ZuAIcRQoSshsg0UBY3NNvYmFGtrpsdzsvAyrMGQBIOZC6vlk6ohHqmwWH2ACI-Y80VhdEMpO3kA/s200/P1010486.JPG "envoyer commandes depuis le shell vers USB")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiNwQdsO3w5IA68bjygu48chvMB5pk5R0lOl1XbbJgXoEVBH3Fs3YE3BEBjVdhd6Wr0ZuAIcRQoSshsg0UBY3NNvYmFGtrpsdzsvAyrMGQBIOZC6vlk6ohHqmwWH2ACI-Y80VhdEMpO3kA/s1600/P1010486.JPG)