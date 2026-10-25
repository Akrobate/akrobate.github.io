---
date: '2012-05-03T14:05:20+02:00'
draft: false
title: Connaitre la position d'un servo moteur
slug: connaitre-position-servo-moteur
tags:
  - arduino
  - electronique
  - informatique
  - servo moteur
  - teensy
categories:
  - Électronique
cover:
  image: https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgBiggci_a8UpbH_bJXD1F7AjOBQABxwtW_SLJP_yknIbdQ4MfmJGZHD7YY1fnDR-GEluK_dZM-PKrPqK_X5LpP9EmmkUsdQ1vQ15VexBYDnloiaSipE3WnzvbJf6G_1jl4yi3YXL5j97A/s200/P1010002.JPG
  alt: "Image d'illustration"
description: No description
showTOC: true
---


### Connaitre la position d'un servo moteur

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgBiggci_a8UpbH_bJXD1F7AjOBQABxwtW_SLJP_yknIbdQ4MfmJGZHD7YY1fnDR-GEluK_dZM-PKrPqK_X5LpP9EmmkUsdQ1vQ15VexBYDnloiaSipE3WnzvbJf6G_1jl4yi3YXL5j97A/s200/P1010002.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgBiggci_a8UpbH_bJXD1F7AjOBQABxwtW_SLJP_yknIbdQ4MfmJGZHD7YY1fnDR-GEluK_dZM-PKrPqK_X5LpP9EmmkUsdQ1vQ15VexBYDnloiaSipE3WnzvbJf6G_1jl4yi3YXL5j97A/s1600/P1010002.JPG)

Les servos moteurs sont une solution simple pour mettre en place la partie mécanique d'un robot ou un automatisme. En effet un servo moteur a du couple (3kg/cm pour un servo moteur standard), une précision quasiment au degré près (selon les modèles) et a une taille convenable pour de l'embarqué. Cependant un servo moteur de modélisme standard n'a pas d'indicateur de position, ce qui signifie que l'on ne sait pas la position à un instant t du servo moteur. Dans cet article je vous propose une solution pour **connaitre a tout moment la position d'un servo moteur**. Il existe des solutions de modification de servo très poussées consistant a remplacer intégralement la carte éléctronique du servo par un microcontrolleur, mais ces solutions sont plus honéreuses a mettre en place. Dans cet article je vous propose une solution consistant a souder un seul fil sur le potentiomètre du servomoteur.  
  
  
  
  
**Commander un servo moteur.**   
  
Pour commander un servo moteur il suffit d'envoyer un signal (positionner la broche de commande du servo moteur à +5V) d'une durée allant de 1ms à 2ms toutes les 20ms. Un signal de 1ms correspond a une extrémité du servo et 2ms correspond a l'autre extrémité du servo moteur.  
  
**Problématique.**  
  
Donc pour commander un servo moteur on lui envoi la position désirée et le servo se positionne. Dans le cadre d'un programme informatique il peut être plus qu'important de **connaitre la position d'un servo moteur**. En effet cette valeur peut servir pour savoir **si le servo moteur a atteint la position** envoyée ou s'il est encore entrain d'effectuer la rotation. En effet dans le cadre d'un robot de type hexapode il peut être utile de savoir les états des servos tout simplement pour savoir a quel moment continuer le mouvement. Effectivement une solution pourrait être de calculer le temps d'exécution d'un mouvement de 0 a 180° afin de prévoir ensuite la position du servo en fonction du temps. Cependant cette technique ne marche plus si par exemple la batterie s'est un peu déchargée, ou alors s'il y a, à ce moment là une contrainte mécanique sur le servo moteur.  
  
**Solution de retour de position par le servo.**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxxSe5IvR4owShzNsZoWX8Hft3MvrgN1bU8ghr3LkWMj4TUUjwEcwqLmqzofAFBfdG8aoCzgdkooJdRh-7UOdlBn4lpMBcDuLb0RP_bfV3bUvDwo76Zra8RAHp3Vde-tV20IeX9hrKxH8/s200/P1010003.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgxxSe5IvR4owShzNsZoWX8Hft3MvrgN1bU8ghr3LkWMj4TUUjwEcwqLmqzofAFBfdG8aoCzgdkooJdRh-7UOdlBn4lpMBcDuLb0RP_bfV3bUvDwo76Zra8RAHp3Vde-tV20IeX9hrKxH8/s1600/P1010003.JPG)

Un servo moteur est constitué d'un moteur avec réducteurs d'une carte électronique et d'un potentiomètre linéaire qui permet à la carte électronique de vérifier la position actuelle du servo. Je vous propose d'utiliser cette **valeur envoyée par le potentiomètre** afin de connaitre la position du servo moteur. En effet le potentiomètre est mécaniquement lié directement au palonnier du servo moteur. Donc la résistance obtenue au bornes du potentiomètre correspond à la position du palonnier.  
  

  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjamAfGwjmf0vOA2C6cFu9JVa2i0F8m78Nln_xIdV7szRppEPROVZvi-RxSgWk0zhbSqunA3XxcCoaCCNSiAXJfu83esSTCx4BULx_yafQcX71X2KF-cd_JAf8T2xIBhWIp_gAuTfmLqA/s200/P1010008.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjamAfGwjmf0vOA2C6cFu9JVa2i0F8m78Nln_xIdV7szRppEPROVZvi-RxSgWk0zhbSqunA3XxcCoaCCNSiAXJfu83esSTCx4BULx_yafQcX71X2KF-cd_JAf8T2xIBhWIp_gAuTfmLqA/s1600/P1010008.JPG)Il suffit pour cela de **souder un fil sur la patte du milieu du potentiomètre**. Ensuite une fois le servo moteur en action, on peut **mesurer la tension** entre la masse en notre nouvelle pin du servo (patte du milieu du potentiomètre) d'environ 0.9V lorsque le palonnier est tourné tout a droite, et 1,7V lorsque le palonnier est tout a gauche.  
  
Le programme informatique devra évidement effectuer un genre d'étalonnage au début de l'exécution. Positionner le servo tout a droite, et voire la valeur du capteur, puis positionner le servo tout a gauche et voir la valeur du capteur. Ces deux valeurs vont nous servir de référence min et max de la variation. En effet la variation mesurée est de 1.7V - 0.9V = 0.8V. Votre entrée analogie doit avoir une définition suffisante pour avoir un peu de précision. En effet sur une variation de 0.8V il s'agit de représenter théoriquement les 180° de rotation. Donc l'entrée analogique devra être capable de reperer des variations de 5mV pour avoir une précision d'environ 1°. Il va de sois qu'il est aussi envisageable d'enregistrer les valeurs minimales et maximales de la tension obtenue au bornes du potar pour ne pas avoir a effectuer l'étalonnage a chaque initialisation.  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjstar5fi-97RHGgkmBQ_dTrEBQJUnOO6B60QbgxYosdx0cjzydE2WMFv2Zn6rgl_vbtCkkgWaXePh2Zv8qM_Ve0O2CEL_6UINx6vlPn6yF1W_Wbz6xSMWgZ2gNe1VLSi8elkMLUegU6j8/s200/P1010015.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjstar5fi-97RHGgkmBQ_dTrEBQJUnOO6B60QbgxYosdx0cjzydE2WMFv2Zn6rgl_vbtCkkgWaXePh2Zv8qM_Ve0O2CEL_6UINx6vlPn6yF1W_Wbz6xSMWgZ2gNe1VLSi8elkMLUegU6j8/s1600/P1010015.JPG)Dans mon exemple j'utilise une entrée analogique d'un teensy 2 ++ (équivalent de l'arduino) pour vérifier la position du servo moteur. Puis cette valeur obtenue est envoyé a l'écran sous forme d'un indicateur.  
Par ailleurs j'utilise la lib officielle de arduino pour commander le servo moteur. Dans ma boucle principale j'effectue bien évidement la mesure du potentiomètre pour indiquer a l'écran la position actuelle du servo moteur.  
Vous pouvez tout a fait aussi déconnecter la patte de la commande du servo et faire tourner a la main le servo moteur, vous verrez alors l'indicateur se déplacer a l'écran indiquant toujours la position actuelle du servo moteur.  
  
  
  

#include 
#include 
  
LiquidCrystal lcd(6, 7, 10, 11, 12, 13);
Servo myservo;
 
int pos = 1;    // variable to store the servo position
int sensorPin = 38;
int sensorValue = 0;
int sense = 1;
int sensorMax = 0;
int sensorMin = 0;
int sensorNorm = 0; 
int sensorOld = 0;

void setup()
{
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
    lcd.begin(16, 2);
}
 
 
void loop()
{   
  myservo.write(1);
  delay(2000);
  sensorMin = analogRead(sensorPin);
  myservo.write(180);
  delay(2000);
  sensorMax = analogRead(sensorPin); 
  lcd.clear();
  lcd.setCursor(4,0);
  lcd.print(String("Min :") + sensorMin);
  lcd.setCursor(4,1);
  lcd.print(String("Max:") + sensorMax);  
  delay(4000);

    while(true) {
     sensorValue = analogRead(sensorPin);
     sensorOld = sensorNorm; 
     sensorNorm = map(sensorValue, sensorMin, sensorMax, 1, 180);
      if ((sensorNorm > 0) && (sensorNorm <= 180)) {
         if (abs(sensorOld - sensorNorm) < 2) {
            lcd.clear();
            lcd.setCursor(0,0);
            lcd.print(indic(sensorNorm));
         }
      }
     
      pos += sense;
      
      if ((pos <= 1) || (pos >= 180)) {
        sense *= -1;
      }
      
      myservo.write(pos);
      delay(10);  
    }
}


String indic(int sensor) {
  String result = "";
  int  sensorNorm = map(sensor, 1, 180, 0, 14); 
   
   result = "[";
   for (int i =0; i < 14; i ++) {
     if (i == sensorNorm) {
       result += "O";
     } else {
       result += "-";
     }
     
   } 
 
 result += "]";
 
 return result;
}

**Documentation annexe**  
  
[http://fribotte.free.fr/bdtech/pic/pic_et_servo.html](http://fribotte.free.fr/bdtech/pic/pic_et_servo.html)  
  
