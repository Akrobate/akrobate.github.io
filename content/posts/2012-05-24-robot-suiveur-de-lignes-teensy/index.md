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
cover:
  image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilRTBDsZWxz8a6xB7PrhWRRaR0-rNMneT5OI66S02OBVAvGPoXwemvsX5YNaN94AVUaqIm0hAwZ_N9VzE0zDm79Q3zPorH0vNRH_QshdIbs8e5Ms891YJGwqAwAjEt0XTXk6ll_PcpJjA/s1600/robot-suiveur-de-lignes-main.JPG"
  alt: "Image d'illustration"
---


### Robot suiveur de lignes a base du teensy (arduino)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilRTBDsZWxz8a6xB7PrhWRRaR0-rNMneT5OI66S02OBVAvGPoXwemvsX5YNaN94AVUaqIm0hAwZ_N9VzE0zDm79Q3zPorH0vNRH_QshdIbs8e5Ms891YJGwqAwAjEt0XTXk6ll_PcpJjA/s200/robot-suiveur-de-lignes-main.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilRTBDsZWxz8a6xB7PrhWRRaR0-rNMneT5OI66S02OBVAvGPoXwemvsX5YNaN94AVUaqIm0hAwZ_N9VzE0zDm79Q3zPorH0vNRH_QshdIbs8e5Ms891YJGwqAwAjEt0XTXk6ll_PcpJjA/s1600/robot-suiveur-de-lignes-main.JPG)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPfrpkeFJJVl7Q_MlpaBbdjVLl9Pz_lydWUkGXVcKvjeBkXYlHqrD_x4AJRfiAizmzOV1JEVHHwkGmSEV4FrKEwyyCbUPnThsn7NMnOOX3i8ka3X_NjhFMlgguKoskN4aWd1VSNhwk1AA/s200/P1010040.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPfrpkeFJJVl7Q_MlpaBbdjVLl9Pz_lydWUkGXVcKvjeBkXYlHqrD_x4AJRfiAizmzOV1JEVHHwkGmSEV4FrKEwyyCbUPnThsn7NMnOOX3i8ka3X_NjhFMlgguKoskN4aWd1VSNhwk1AA/s1600/P1010040.JPG)Le **robot suiveur de lignes** est un petit projet très simple. On trace une ligne au feutre noir sur une grande feuille blanche on pose le robot sur la ligne, et ce dernier va suivre la ligne. Ici mon robot fonctionne avec un Teensy 2 ++ (équivalent de l'**arduino** mais avec des ports entrés/sorties en plus) cadencé a **16Mhz**. Le châssis utilisé est en légos technics, et pour la motorisation j'ai utilisé les **moteurs lego** power functions. Les lignes sont détectées grâce a deux **capteurs de lignes** basés sur des photo résistance. L'astuce principale de ce robot réside dans l'**utilisation de l'infrarouge pour commander les moteurs** officiels légo. Cela permet de ne pas avoir la moindre interface "physique" entre le circuit contrôleur et l'étage de la motorisation. Le robot suiveur de lignes possede donc deux parties electroniques distinctes. D'un coté les lego power functions (motorisation légo), et de l'autre le circuit de la plaque a essai qui est alimenté par une batterie de 9v.

  
  
**Le châssis et les capteurs.**  
  
Le châssis est entièrement réalisé en lego technics issus du set 8275. C'est un bulldozer de lego technics. Ce set comprenait pas mal de pièces intéressantes pour la robotique: 4 moteurs deux récepteurs infrarouges, un pack alimentation et une télécommande infrarouge. Par ailleurs étant donné qu'il s'agit d'un bulldozer le set comprends des chenilles très pratiques pour la motorisation. Pour commander cette base en légo j'émule les signaux de la télécommande officielle en utilisant ma classe arduino LegoRC. Je vous invite a lire l'article sur la [télécommande lego power function et librairie arduino](http://artiom-fedorov.blogspot.fr/2012/05/telecommande-infrarouge-lego-power.html) pour mieux comprendre les détail de l'interface. Donc l'interface entre l'arduino et le châssis lego se limite a une diode infrarouge orientée vers le récepteur lego power functions.  
Les capteurs de lignes sont simplifiés au maximum. En effet il ne s'agit que d'une simple photo résistance et une diode d'éclairage. Je vous invite aussi a lire l'[article sur ce capteur de lignes](http://artiom-fedorov.blogspot.fr/2012/05/capteur-de-lignes-pour-la-robotique-et.html), et surtout la classe LineSensor pour arduino, qui permet d'utiliser très simlement ce capteur.  
En ce qui concerne la fixation de la plaque a essai le hasard fait bien les choses ci bien que une des fixations standard de légo rentre pile poil dans les quartes trous dont la plaque a essai est munie. C'est une [plaque a essai relativement basique achetée chez SELECTRONIC](http://www.selectronic.fr/plaque-d-essais-550-points.html).  
  
**Quelques photos du robot**  
  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8QT-2Sc6jc8zSdHb47kbtYoq8YzgkN7Cnm9m8uv4XhpmuVfXPmpiQtsK_xM8YoWiBfc05BBkSv-9u49n70ubouvoYxb-HH9uQ9i0489ei2iGC9oMPSVt9DbBRohxOsR5lnvLJ1Yg7-ZQ/s200/P1010052.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8QT-2Sc6jc8zSdHb47kbtYoq8YzgkN7Cnm9m8uv4XhpmuVfXPmpiQtsK_xM8YoWiBfc05BBkSv-9u49n70ubouvoYxb-HH9uQ9i0489ei2iGC9oMPSVt9DbBRohxOsR5lnvLJ1Yg7-ZQ/s1600/P1010052.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjRIUYLzf-DPRTOVDlRxD1cTfhhuySwKjSg47liH8JE__dnRAgdcrj6sjyu0f9ieKmm3C-rQXy8610m_y36zT3kTzonDqHTC6qxGDOPmiLKTivswJc5z2IMYTiF1SQrR21sClQJm3SyXng/s200/P1010053.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjRIUYLzf-DPRTOVDlRxD1cTfhhuySwKjSg47liH8JE__dnRAgdcrj6sjyu0f9ieKmm3C-rQXy8610m_y36zT3kTzonDqHTC6qxGDOPmiLKTivswJc5z2IMYTiF1SQrR21sClQJm3SyXng/s1600/P1010053.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYZSUZDiJlGeab-pA3zNAGKPG86TN4f6Uh2zwXzHt7HEE1Zfsvl0_cmH8i9KW_xPB4Fb-jAJY252njDRev3EjVZcqXEAeIOFujb9pJ5CLhGZDn_kU3ZXK6mprT1EFK9GusNC5QCAjhzcc/s200/P1010055.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYZSUZDiJlGeab-pA3zNAGKPG86TN4f6Uh2zwXzHt7HEE1Zfsvl0_cmH8i9KW_xPB4Fb-jAJY252njDRev3EjVZcqXEAeIOFujb9pJ5CLhGZDn_kU3ZXK6mprT1EFK9GusNC5QCAjhzcc/s1600/P1010055.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQMSbW273GXtQgmrdPVIpzChKnlY1TxouOUZGDGz8knLXvC_Wi9CiSrfNOfopgE8ycWCWyt5CfeK-VeV4BEJJRLkQiflVp0bRvptwuse81lvz9tTIOiEz9KzfV_dDd0kweDuVLLmF6U9U/s200/P1010054.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQMSbW273GXtQgmrdPVIpzChKnlY1TxouOUZGDGz8knLXvC_Wi9CiSrfNOfopgE8ycWCWyt5CfeK-VeV4BEJJRLkQiflVp0bRvptwuse81lvz9tTIOiEz9KzfV_dDd0kweDuVLLmF6U9U/s1600/P1010054.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiCu0aD5Lxeh1Pu_UJyMSsNtVSsY2Ff7lzfO0cvOe0MSml_vCgWWB3sEnBDIpbtqs1tTw-9N93Z3MGzP4qnmnzSemW4iIthd7DgL1xvVDWOs23wl7v6IDoHL_de6QkkEmKwtrZjLuEmNj0/s200/P1010042.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiCu0aD5Lxeh1Pu_UJyMSsNtVSsY2Ff7lzfO0cvOe0MSml_vCgWWB3sEnBDIpbtqs1tTw-9N93Z3MGzP4qnmnzSemW4iIthd7DgL1xvVDWOs23wl7v6IDoHL_de6QkkEmKwtrZjLuEmNj0/s1600/P1010042.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgPPd-VJ3-Avmw55aAQNf86ccw2Yjfp3EtE-lVi19oFlz6-lcMAj9XwryiBB1IgZWWMRQ_sqxhUTWbmCn6jeJFXAiI-EYXa1zEaAs_FBF5rGredLjd5F2MNMwTnPPU-5h5F9kJuUajUF4/s200/P1010041.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgPPd-VJ3-Avmw55aAQNf86ccw2Yjfp3EtE-lVi19oFlz6-lcMAj9XwryiBB1IgZWWMRQ_sqxhUTWbmCn6jeJFXAiI-EYXa1zEaAs_FBF5rGredLjd5F2MNMwTnPPU-5h5F9kJuUajUF4/s1600/P1010041.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPfrpkeFJJVl7Q_MlpaBbdjVLl9Pz_lydWUkGXVcKvjeBkXYlHqrD_x4AJRfiAizmzOV1JEVHHwkGmSEV4FrKEwyyCbUPnThsn7NMnOOX3i8ka3X_NjhFMlgguKoskN4aWd1VSNhwk1AA/s200/P1010040.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPfrpkeFJJVl7Q_MlpaBbdjVLl9Pz_lydWUkGXVcKvjeBkXYlHqrD_x4AJRfiAizmzOV1JEVHHwkGmSEV4FrKEwyyCbUPnThsn7NMnOOX3i8ka3X_NjhFMlgguKoskN4aWd1VSNhwk1AA/s1600/P1010040.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirfwL7b5UEar_unoW3g0MuStUQCm8cUK0k43na_E6RFNGLpS6gGXbrsAOucn5AmaFzdFEuufBbjaWdGt2zt5bYCiwp2_smfPZgY7hUlzF-UDQFwS_XUEOftty6ZixJe-fqm2bo0jK7RVY/s200/P1010039.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirfwL7b5UEar_unoW3g0MuStUQCm8cUK0k43na_E6RFNGLpS6gGXbrsAOucn5AmaFzdFEuufBbjaWdGt2zt5bYCiwp2_smfPZgY7hUlzF-UDQFwS_XUEOftty6ZixJe-fqm2bo0jK7RVY/s1600/P1010039.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh2RYWLyXw_rrJukw2PtX8tvS8Csp15WBUDG1KwQhgVmtpTon4IZ0lvm5Sw2rVtmnJe5r1eFQQjdAI32hgtXmPlk03JOOzBgGlVc-CbSMSLqx7HW2lKO7e-DlnPQ9gy2KMpi1rKM1C6GBY/s200/P1010038.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh2RYWLyXw_rrJukw2PtX8tvS8Csp15WBUDG1KwQhgVmtpTon4IZ0lvm5Sw2rVtmnJe5r1eFQQjdAI32hgtXmPlk03JOOzBgGlVc-CbSMSLqx7HW2lKO7e-DlnPQ9gy2KMpi1rKM1C6GBY/s1600/P1010038.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUVHqjjypC7aRA1GXjHAvuT1p_oWHTOmtQ8NSeZlH41X91agUcD_gYuTOBcV5jY1f6_G0t5-o3Ax_KU5NKXJhyphenhyphen8tytDoCDzJ7w_phMlvq2tiwkXHGymQ5KEq8fhcONPhA9OtQL1PnDs-s/s200/P1010037.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUVHqjjypC7aRA1GXjHAvuT1p_oWHTOmtQ8NSeZlH41X91agUcD_gYuTOBcV5jY1f6_G0t5-o3Ax_KU5NKXJhyphenhyphen8tytDoCDzJ7w_phMlvq2tiwkXHGymQ5KEq8fhcONPhA9OtQL1PnDs-s/s1600/P1010037.JPG)  

  
  
**Le programme informatique.**  
  
Le programme informatique pour l'arduino est très simple. On commence par déclarer les capteurs avec en paramètre la broche sur laquelle est branché le capteur. Ensuite on déclare l'objet LegoRC qui permet de communiquer simplement avec les moteurs. Dans la boucle principale on vérifie les capteurs. Si les deux capteurs ne détectent pas de ligne alors le robot avance. Si un des capteurs est actif alors le robot pivote sur lui meme jusqu'a ce que le capteur ne detecte plus à nouveau la ligne.  
  

// inlcuding libs
#include "LineSensor.h"
#include "LegoRC.h"

// Declaration des sensors
LineSensor rightLineSensor(38);
LineSensor leftLineSensor(39);

//Declaration de la motorisation chassis
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

  
  
**L'electronique : schemas.**  
  
Le schémas électronique du robot est on ne peut plus simple. Le montage utilise un teensy2++ équivalent de l'arduino. Le schémas électronique proposé ci dessous utilise le brochage déclaré dans le programme du robot. Sur le schémas vous pouvez voir la partie alimentation a base d'un 7805 standart. En effet l'alimentation de la carte est assuré par une batterie de 9v. On n'utilise pas ici l'alimentation des moteurs. Notre carte a sa propre partie alimentation.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiKck98zgHZ1ElcpiVtg5aOl5Hc88GyVIrHkBPaePADzWjnGV9HWP-2UhzN07LxAehuZQRFAHSZ7mU4pKTjGrz9XmgeCJSccFOkfl1m0avzW35_1CPdIdxTD6RlNv40QFAPwry3TFVKxq8/s640/RobotLineFollower.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiKck98zgHZ1ElcpiVtg5aOl5Hc88GyVIrHkBPaePADzWjnGV9HWP-2UhzN07LxAehuZQRFAHSZ7mU4pKTjGrz9XmgeCJSccFOkfl1m0avzW35_1CPdIdxTD6RlNv40QFAPwry3TFVKxq8/s1600/RobotLineFollower.png)

  
  
**Planning de gant du projet Robot suiveur de lignes.**  
  
Enfin pour finir, un petit bonnus: J'utilise souvent pour encadrer mes projets le diagramme de gant qui permet de lister les tâches à réaliser puis de déterminer l'enchainement des tâches. Le diagramme de gant permet de s'organiser rapidement et savoir par quoi commencer en fonction des enchainements possibles une fois une tache achevée. Je vous invite a vous renseigner sur cette méthode d'organisation qui permet d'être plus efficace dans des projets ayant de nombreux axes de développement.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjFVS-IsP4xWQ4X-chR_Cuzt62T19lfB0ZBskOsD0N6bpPLdtk-P4lu-QqQrmDbFhd7QbQwt8E4keFBW4jfnYvFbP7QCeInNwmOJQexXiYnfoDS9pdzJyq9UWkOmR-sQtGuhmQ-bHfVm38/s640/gant+robot.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjFVS-IsP4xWQ4X-chR_Cuzt62T19lfB0ZBskOsD0N6bpPLdtk-P4lu-QqQrmDbFhd7QbQwt8E4keFBW4jfnYvFbP7QCeInNwmOJQexXiYnfoDS9pdzJyq9UWkOmR-sQtGuhmQ-bHfVm38/s1600/gant+robot.png)

  
  
**Vidéo du robot en fonctionnement**  
  
  
  

  
  
  
**Documents annexes**  
  
[Code source complet du projet robot suiveur de lignes arduino](http://artiom21.free.fr/projets/arduino-robot-line-follower/RobotLineFollow.zip)  
[Documentation sur l'interface arduino - lego (LegoRC arduino class)](http://artiom-fedorov.blogspot.fr/2012/05/telecommande-infrarouge-lego-power.html)  
[Documentation sur les capteurs de lignes et classe arduino](http://artiom-fedorov.blogspot.fr/2012/05/capteur-de-lignes-pour-la-robotique-et.html)