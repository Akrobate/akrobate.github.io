---
date: '2026-09-25T14:05:20+02:00'
draft: false
title: "Robot suiveur de balles OpenCV (Projet expérimental)"
slug: "robot-suiveur-de-balles"
tags:
  - arduino
  - Artiom FEDOROV
  - electronique
  - informatique
  - lego
  - lego power functions
  - OpenCV
  - robot
  - robotique
  - teensy
  - telecommande lego
  - telecommande RC
categories:
  - Électronique
cover:
  image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s1600/P1010494.JPG"
  alt: "Image d'illustration"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s200/P1010494.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s1600/P1010494.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgu56h8jiiC7kxQUyDIdqiJoJp9s-lw1vk3cECOkydorksJw9LAkCqJGN5XqonjbzariwwesuTMUi8gNIYn7vtyds2W02a6UMaf2g6iCN7umbazdqC4T86eAKHmKnretIqMTyQJmw66U0/s200/P1010487.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgu56h8jiiC7kxQUyDIdqiJoJp9s-lw1vk3cECOkydorksJw9LAkCqJGN5XqonjbzariwwesuTMUi8gNIYn7vtyds2W02a6UMaf2g6iCN7umbazdqC4T86eAKHmKnretIqMTyQJmw66U0/s1600/P1010487.JPG)Le projet robot tourelle suiveuse de balles, est sans doutes le premier d'une longue série de petits projets à venir. En effet les possibilités offertes par la librairie **OpenCV** sont impressionnantes et "simples" à mettre en place. L'idée de ce premier projet à base d'**OpenCV** est de réussir à déplacer une webcam montée sur un châssis rotatif afin que celle ci fixe une balle et la centre au milieu de l'image. Le châssis est entièrement réalisé en légos et la caméra est une petite webcam générique maintenue en place sur une pièce légo par des visses. La motorisation est un kit power functions contenant deux petits moteurs, le bloc batterie et le récepteur infrarouge légo. La webcam est branchée directement à un PC. La tourelle quand à elle est branchée aussi à l'USB grâce à une interface "maison" USB vers signaux infrarouges légo. Côté commande de la tourelle il suffit d'envoyer des chaines de caractères (correspondant à la rotation moteur voulue) dans le bon périphérique usb.  
  

**Partie électronique du projet**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQU9mc9Q1aO-TRLOYNW9MxF5VSeImVCk21jAYkUyCkKCX809fXBUl-Dlit7W6KOcGfvIpw2Ac76UGD0kunWKYu_AO26LwmVhzqL9FGo3dYKu9IYjlm887MNxq-LxCBnT-1CxCX4VM1UXc/s200/recepteur+infrarouge+artiom+fedorov.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQU9mc9Q1aO-TRLOYNW9MxF5VSeImVCk21jAYkUyCkKCX809fXBUl-Dlit7W6KOcGfvIpw2Ac76UGD0kunWKYu_AO26LwmVhzqL9FGo3dYKu9IYjlm887MNxq-LxCBnT-1CxCX4VM1UXc/s1600/recepteur+infrarouge+artiom+fedorov.JPG)

[![Schemas électronique de l'intérface USB vers Signaux infrarouges légo](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhm5QYoc4il_JOgmrAARchixV3VGqRjbliCOtKLRmh8TiY_a3p6sBpuYaiaxjc4wElGjZjmcjRvHe4S5xYqyDgsiiaK2npg4OnbNccVkqX9rZuoYToeKaiIbaz9kUsP1BzQwlBGxSdCCTY/s200/USBversLegoCommand.png "Schemas electronique interface lego IR usb")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhm5QYoc4il_JOgmrAARchixV3VGqRjbliCOtKLRmh8TiY_a3p6sBpuYaiaxjc4wElGjZjmcjRvHe4S5xYqyDgsiiaK2npg4OnbNccVkqX9rZuoYToeKaiIbaz9kUsP1BzQwlBGxSdCCTY/s1600/USBversLegoCommand.png)La partie électronique du projet se résume en quelques composants très basiques ainsi que des concepts précédemment évoqués sur mon blog. En effet la partie électronique nécessaire est l'interface entre l'USB et la commande infrarouge légo. Donc au final c'est un mélange entre le projet [Télécommande infrarouge lego power function et librairie arduino](http://artiom-fedorov.blogspot.fr/2012/05/telecommande-infrarouge-lego-power.html) (pour toute la partie génération des signaux infrarouges et commande des moteurs) et [Mini écran LCD pour serveur (linux) en USB](http://artiom-fedorov.blogspot.fr/2012/09/futur-articlemini-ecran-lcd-pour.html) (pour tout ce qui concerne la lecture des chaines de caractères sur le port USB. Le coeur de la partie électronique est un teensy2++ (équivalent de l'arduino). Ce circuit en lui même est on ne peut plus simple. J'ai choisi de conserver le **montage du mini écran LCD en USB** pour ce projet car cela permet d'avoir un debug supplémentaire sous la main.

  

Le schéma électronique ne change quasiment pas du schéma du mini écran LCD pour usb. En effet la seule évolution c'est le **rajout de la diode infrarouge** et de sa résistance pour l'envoi des commandes infrarouges vers le récepteur de Lego.

  
**Le programme informatique de l'adaptateur USB vers commande infrarouge lego**  
  
Le programme est très simple. La boucle principale s'occupe de **lire les messages séries** arrivant **par le port USB** puis de les **retranscrire en signaux légo** grâce a la classe Lego détaillée dans l'[article télécommande infrarouge lego power function](http://artiom-fedorov.blogspot.fr/2012/05/telecommande-infrarouge-lego-power.html). Les messages USB sont eux générés par un autre programme tournant cette fois ci sur le PC. Dans le programme du teensy (équivalent arduino) vous pouvez voir une méthode permettant d'utiliser l'écran LCD pour **afficher** ce qui se passe en ce qui concerne **la réception des messages en USB**. Cette phase est évidement chronophage,  de ce fait si on cherche a optimiser la fluidité de transmission de notre interface il s'agira de commenter tout ce qui commence par lcd dans la fonction sendRc.  
  

#include <liquidcrystal.h>
#include "LegoRC.h"

LegoRC legoRC(2, 50);
LiquidCrystal lcd(24, 25, 8, 9, 27, 0);
String l1="", l2="", tmpl="";
char incomingByte;
int newMSG = 0;
int led = 12;

void setup() {
  pinMode(led, OUTPUT);
  lcd.begin(16, 2);
  Serial.begin(9600);
}


void loop() {
  // Lecture d'une chaine de carracteres
  while (Serial.available()) {
    digitalWrite(led, HIGH);
    incomingByte = Serial.read();  // will not be -1
    tmpl = tmpl + char(incomingByte);
    newMSG = 1;
  }

   digitalWrite(led, LOW);

    if (newMSG) {
      l1 = l2;
      l2 = tmpl.trim();
      String  myString = l2;
      int myStringLength = myString.length()+1;
      char myChar[myStringLength];
      myString.toCharArray(myChar,myStringLength);
      int result = atoi(myChar);
      sendRc(result);
      tmpl = "";      
    }

    newMSG = 0;
}


void sendRc(int i) {
 
 int m1 = i / 100;
 int m2 = i % 100;
 
 lcd.clear();
 lcd.setCursor(0, 0);
 lcd.print(m1);   

 lcd.setCursor(0, 1);
 lcd.print(m2);   
  
 legoRC.sendCommand(4, m1, m2);

}

  
**Le programme informatique côté PC**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvVn8bP4Fv48quVcrpUFejuIVxwNTJBF86gHoiMU310G2UdszJL37_6-x2TXQyouYYfVpC4bxOacvKAeXFudW9WIGLwlS77fnAPp1FEpJciz7c35D9x8dWXl2pIKrLBceyHr_ShYiku8Q/s200/P1010492.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvVn8bP4Fv48quVcrpUFejuIVxwNTJBF86gHoiMU310G2UdszJL37_6-x2TXQyouYYfVpC4bxOacvKAeXFudW9WIGLwlS77fnAPp1FEpJciz7c35D9x8dWXl2pIKrLBceyHr_ShYiku8Q/s1600/P1010492.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjtX6B84y11tnvb8KIBb4cUOR3cBaT2nnlwo6J4qFcC-AlFlt2nN7sS3HLcG-Eoublvi87BYIgueTlCRZP0G9RhMfaR-XWh6j3ambRmQ5UMXgqjVtw0UjvZMfaRyOlf28z0F4WHuMupeb4/s200/detection+cercles+open+cv+artiom.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjtX6B84y11tnvb8KIBb4cUOR3cBaT2nnlwo6J4qFcC-AlFlt2nN7sS3HLcG-Eoublvi87BYIgueTlCRZP0G9RhMfaR-XWh6j3ambRmQ5UMXgqjVtw0UjvZMfaRyOlf28z0F4WHuMupeb4/s1600/detection+cercles+open+cv+artiom.png)Côté PC un programme en C permet la détection de ronds a la webcam et indique la correction nécessaire pour amener le rond détecté au centre de l'image de la webcam. La détection de cercles dans l'image se fait grâce a la librairie OpenCV.  
  
La libraire openCV propose la fonction _HoughCircles_ permettant de détecter tous les cercles reconnus à l'image. Pour chaque cercle les coordonnées x et y ainsi que le rayon du cercle détecté sont renvoyés par la fonction. Dans mon code je pars du principe qu'un seul cercle est présent a l'image, si tel n'est pas le cas, alors je prends le cercle qui a été détecté en dernier dans l'image courante. Une fois que nous disposons des coordonnées (x,y) du cercle détecté, nous pouvons donc e**stimer la direction de la rotation** de la tourelle afin que **x et y soient le plus proche possible du centre de l'image**. Dans le code j'ai implémenté une variable servant d'erreur acceptée afin qu'un déplacement minime du cercle dans la vision de la webcam ne déclenche pas une rotation de la tourelle. Ce procédé me permet d'éviter la réaction de la tourelle au bruit induit par la **détection des cercles par OpenCV**.  
  

#include "stdio.h"
#include "opencv/cv.h"
#include <math.h>
#include "opencv/highgui.h"

void xl();
void xr();
void yt();
void yb();
void xys();

using namespace cv;

int main() {

    VideoCapture cap(1); // open the default camera
    if(!cap.isOpened())  // check if we succeeded
        return -1;

    Mat edges;
    namedWindow("edges",1);

    int circlex = 0;
    int circley = 0;
    int bbox = 0;

    for(;;)
    {
        Mat frame;
        cap >> frame; // get a new frame from camera
        cvtColor(frame, edges, CV_BGR2GRAY);
        GaussianBlur(edges, edges, Size(9,9), 2, 2);
       
        vector<vec3f> circles;
        HoughCircles(edges, circles, CV_HOUGH_GRADIENT, 2, edges.rows/4, 200, 100 );


       if (circles.size() > 0) {
       
           for (int i = 0; i < circles.size(); i++) {
            circlex = cvRound(circles[i][0]);
            circley = cvRound(circles[i][1]);
            Point center(cvRound(circles[i][0]), cvRound(circles[i][1]));
            int radius = cvRound(circles[i][2]);
            circle(frame, center, 3, Scalar(0,255,0), -1, 8, 0 );
            circle( frame, center, radius, Scalar(0,0,255), 3, 8, 0 );
            printf("x %d ; y %d \n", cvRound(circles[i][0]), cvRound(circles[i][1]) );

           }
            bbox = 20;
            if (circlex > (320 + bbox)) {
                xr();
                xys();

            } else if ((circlex < (320 - bbox)) && (circlex != 0)) {
                xl();
                xys();
            }

            if (circley > (240 + bbox)) {
                yb();
                xys();

            } else if ((circley < (240-bbox)) && (circley != 0)) {
                yt();
                xys();
            }
            
        } else {
            circlex = 0;
            circley = 0;
        }

        imshow("edges", frame);
        
        if(waitKey(30) >= 0) break;
    }
 
    return 0;
}

void xl() {
    system("echo \"408\" > /dev/ttyACM0");
}

void xr() {
    system("echo \"1208\" > /dev/ttyACM0");
}

void yt() {
    system("echo \"812\" > /dev/ttyACM0");
}

void yb() {
    system("echo \"804\" > /dev/ttyACM0");
}

void xys() {
    system("echo \"808\" > /dev/ttyACM0");
}

  
  
**Partie mécanique en légos technics et Lego Power functions**  
  
La mécanique de ce robot suiveur de balles est entièrement faite en légos technics. Seule la caméra usb est fixé sur une pièce légo standard avec des vices. Le principe est simple. La caméra peut tourner a droite ou a gauche en actionnant un des deux petits moteurs des power functions. L'autre moteur sert a la commande monter et descendre la caméra. Les deux moteurs sonts reliés a un récepteur infrarouge (première version) Légo. Le récepteur en lui même est évidement connecté a un bloc d'alimentation légo. Le récepteur infrarouge dervé évidement être mis en face de la diode infrarouge qui émet les signaux transmis par le programme PC via le port USB. La webcam utilisée dans ce projet est une simple caméra usb générique acheté une quinzaine d'euros dans une boutique d'informatique. J'ai privilégié ce modèle pour la facilité de fixation.  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgYDZYfWJRKt7DYSI3aYI2cU_pZDRB5bcKloUVuNb3IgrKOBeQGBF9leJL3kwAP4dJUgK6SHxM54rO9DY7KiK3viFEzzJEq42JK6cAEqPxLO1DAK_27o-lcc60VuS9BsjmGErrVQ2zeMrM/s200/P1010493.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgYDZYfWJRKt7DYSI3aYI2cU_pZDRB5bcKloUVuNb3IgrKOBeQGBF9leJL3kwAP4dJUgK6SHxM54rO9DY7KiK3viFEzzJEq42JK6cAEqPxLO1DAK_27o-lcc60VuS9BsjmGErrVQ2zeMrM/s1600/P1010493.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s200/P1010494.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s1600/P1010494.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHymtCLJA8DRIRJ5ioKa-BzVZTm14yDYRbPZD1R3AbYz1KR0gyQ52uZ-jjat8sozDda09arjWVvjiA0_dV2wqzej0upuGam7-wm9nrh3FrtSx1KxSBBburLDHYQD8bEbKO1JaTVDMcijQ/s200/P1010489.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHymtCLJA8DRIRJ5ioKa-BzVZTm14yDYRbPZD1R3AbYz1KR0gyQ52uZ-jjat8sozDda09arjWVvjiA0_dV2wqzej0upuGam7-wm9nrh3FrtSx1KxSBBburLDHYQD8bEbKO1JaTVDMcijQ/s1600/P1010489.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3oYwnmihLOT9C8YlCFlzbzWE66jqXRxonA76r5BqWqtiJjPamG21hvKb-GteCt7Yr1ettMdlbsyUAqUdMaRBcv_EG-v8HlFQuRVC5RkFtykE8R9A04Goo4c6P2XOk1HYNRrRIxiYjHT0/s200/P1010495.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3oYwnmihLOT9C8YlCFlzbzWE66jqXRxonA76r5BqWqtiJjPamG21hvKb-GteCt7Yr1ettMdlbsyUAqUdMaRBcv_EG-v8HlFQuRVC5RkFtykE8R9A04Goo4c6P2XOk1HYNRrRIxiYjHT0/s1600/P1010495.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhA2W-a2oMGheY1PDhyphenhyphenbHASnrfQ0IiscjDn8zJTZ1vjRtDRzq0aPIWxsKzLTG16NCxJick1dNP-lrv7G3Q9S3dav4oASUK2DVZkRNoVyEtNPbDZnW-rhRgPyUnZ42O6S0hOK70eQq2kOvc/s200/P1010488.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhA2W-a2oMGheY1PDhyphenhyphenbHASnrfQ0IiscjDn8zJTZ1vjRtDRzq0aPIWxsKzLTG16NCxJick1dNP-lrv7G3Q9S3dav4oASUK2DVZkRNoVyEtNPbDZnW-rhRgPyUnZ42O6S0hOK70eQq2kOvc/s1600/P1010488.JPG)  

  
  
**Fichiers du projet robot suiveur de balles a télécharger**  
  
[Code source complet arduino de l'adaptateur USB vers commande légo infrarouge](http://artiom21.free.fr/projets/robot-tourelle-lego/UsbLegoControl.zip)  
[Code source complet C programme de détection opencv et envoi USB (code::blocks)](http://artiom21.free.fr/projets/robot-tourelle-lego/OpenCV.zip)  
  
**Toutes les photos du projet robot suiveur de balles**  
  
[![photos représantant le robot suiveur de balles](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgu56h8jiiC7kxQUyDIdqiJoJp9s-lw1vk3cECOkydorksJw9LAkCqJGN5XqonjbzariwwesuTMUi8gNIYn7vtyds2W02a6UMaf2g6iCN7umbazdqC4T86eAKHmKnretIqMTyQJmw66U0/s200/P1010487.JPG "Robot suiveur de balles")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgu56h8jiiC7kxQUyDIdqiJoJp9s-lw1vk3cECOkydorksJw9LAkCqJGN5XqonjbzariwwesuTMUi8gNIYn7vtyds2W02a6UMaf2g6iCN7umbazdqC4T86eAKHmKnretIqMTyQJmw66U0/s1600/P1010487.JPG)[![robot tourelle suiveur de balles](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhA2W-a2oMGheY1PDhyphenhyphenbHASnrfQ0IiscjDn8zJTZ1vjRtDRzq0aPIWxsKzLTG16NCxJick1dNP-lrv7G3Q9S3dav4oASUK2DVZkRNoVyEtNPbDZnW-rhRgPyUnZ42O6S0hOK70eQq2kOvc/s200/P1010488.JPG "robot suiveur de balles")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhA2W-a2oMGheY1PDhyphenhyphenbHASnrfQ0IiscjDn8zJTZ1vjRtDRzq0aPIWxsKzLTG16NCxJick1dNP-lrv7G3Q9S3dav4oASUK2DVZkRNoVyEtNPbDZnW-rhRgPyUnZ42O6S0hOK70eQq2kOvc/s1600/P1010488.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHymtCLJA8DRIRJ5ioKa-BzVZTm14yDYRbPZD1R3AbYz1KR0gyQ52uZ-jjat8sozDda09arjWVvjiA0_dV2wqzej0upuGam7-wm9nrh3FrtSx1KxSBBburLDHYQD8bEbKO1JaTVDMcijQ/s200/P1010489.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHymtCLJA8DRIRJ5ioKa-BzVZTm14yDYRbPZD1R3AbYz1KR0gyQ52uZ-jjat8sozDda09arjWVvjiA0_dV2wqzej0upuGam7-wm9nrh3FrtSx1KxSBBburLDHYQD8bEbKO1JaTVDMcijQ/s1600/P1010489.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQXPh36gZ0mH3xWozQNkyIOlTaNIWOONlN8r_f2-SoeR94H6qlPcrqBkhyMGMGQdXLGMdIzh1puziMHgD8RgV6USPCltUUNsNzzXmMDiy_gB9LhUfSjsROgkA7j2hcnEVckmnzac6u19Y/s200/P1010490.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQXPh36gZ0mH3xWozQNkyIOlTaNIWOONlN8r_f2-SoeR94H6qlPcrqBkhyMGMGQdXLGMdIzh1puziMHgD8RgV6USPCltUUNsNzzXmMDiy_gB9LhUfSjsROgkA7j2hcnEVckmnzac6u19Y/s1600/P1010490.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s200/P1010494.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXzGVroSXz94N3xPVKDv1QGiMSwramHe91DlRMjHTFrD4LYzRvI83N3AgeVdbOgcj4a_Z9mN1GtChAYBM1otZ2yeHc_qcdGW72kkG25mOhbY0MwTes_ThAM3tQ8JMryMcIkut3UA0-Et4/s1600/P1010494.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgYDZYfWJRKt7DYSI3aYI2cU_pZDRB5bcKloUVuNb3IgrKOBeQGBF9leJL3kwAP4dJUgK6SHxM54rO9DY7KiK3viFEzzJEq42JK6cAEqPxLO1DAK_27o-lcc60VuS9BsjmGErrVQ2zeMrM/s200/P1010493.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgYDZYfWJRKt7DYSI3aYI2cU_pZDRB5bcKloUVuNb3IgrKOBeQGBF9leJL3kwAP4dJUgK6SHxM54rO9DY7KiK3viFEzzJEq42JK6cAEqPxLO1DAK_27o-lcc60VuS9BsjmGErrVQ2zeMrM/s1600/P1010493.JPG)[![detection de cercles par artiom fedorov](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvVn8bP4Fv48quVcrpUFejuIVxwNTJBF86gHoiMU310G2UdszJL37_6-x2TXQyouYYfVpC4bxOacvKAeXFudW9WIGLwlS77fnAPp1FEpJciz7c35D9x8dWXl2pIKrLBceyHr_ShYiku8Q/s200/P1010492.JPG "detection de forme opencv arduino")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvVn8bP4Fv48quVcrpUFejuIVxwNTJBF86gHoiMU310G2UdszJL37_6-x2TXQyouYYfVpC4bxOacvKAeXFudW9WIGLwlS77fnAPp1FEpJciz7c35D9x8dWXl2pIKrLBceyHr_ShYiku8Q/s1600/P1010492.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiWn0JCyxCeOHRXUHWdhkj5kb2Bqr4FyBpukady0_dbdzZ_3j-vxx8gQ1MqJqy8Gd1Zw5mrPVM9rSsDy3uGrTss7sYFhaWusyJUHgLD5F1IFGYkATlGMd6aQWMxOx8cZbnElC1lNDS_dN8/s200/P1010491.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiWn0JCyxCeOHRXUHWdhkj5kb2Bqr4FyBpukady0_dbdzZ_3j-vxx8gQ1MqJqy8Gd1Zw5mrPVM9rSsDy3uGrTss7sYFhaWusyJUHgLD5F1IFGYkATlGMd6aQWMxOx8cZbnElC1lNDS_dN8/s1600/P1010491.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3oYwnmihLOT9C8YlCFlzbzWE66jqXRxonA76r5BqWqtiJjPamG21hvKb-GteCt7Yr1ettMdlbsyUAqUdMaRBcv_EG-v8HlFQuRVC5RkFtykE8R9A04Goo4c6P2XOk1HYNRrRIxiYjHT0/s200/P1010495.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3oYwnmihLOT9C8YlCFlzbzWE66jqXRxonA76r5BqWqtiJjPamG21hvKb-GteCt7Yr1ettMdlbsyUAqUdMaRBcv_EG-v8HlFQuRVC5RkFtykE8R9A04Goo4c6P2XOk1HYNRrRIxiYjHT0/s1600/P1010495.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgZu-mMf6hprVS4EwGlXB0Vlerv7hTmyGMqP7btp2eOWihzP0jahXrL6KPFpw0gSUKknhYFR1SUUK1tQeoNljK8TLBqOniAl_z2AL_-dPTMrRiE0m1NYwupzhxb5LB4nnda6r92CH3noIU/s200/P1010496.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgZu-mMf6hprVS4EwGlXB0Vlerv7hTmyGMqP7btp2eOWihzP0jahXrL6KPFpw0gSUKknhYFR1SUUK1tQeoNljK8TLBqOniAl_z2AL_-dPTMrRiE0m1NYwupzhxb5LB4nnda6r92CH3noIU/s1600/P1010496.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiS062j3z1gIM3oqNXjkndflbibnciv7uYcQYifzXqVj7CUIYpczQWDdGA5doN79fSP1_u4kDZWI4OnzrD9VYvt_3mMIjEeqBft1S451f9JoGcLbEN50avlM6Qg2QL3T8LFH5B-D1oUkNU/s200/P1010497.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiS062j3z1gIM3oqNXjkndflbibnciv7uYcQYifzXqVj7CUIYpczQWDdGA5doN79fSP1_u4kDZWI4OnzrD9VYvt_3mMIjEeqBft1S451f9JoGcLbEN50avlM6Qg2QL3T8LFH5B-D1oUkNU/s1600/P1010497.JPG)