---
date: '2026-09-25T14:05:20+02:00'
draft: false
title: "Interface télécommande RC en Joystick USB"
slug: "interface-telecommande-rc"
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
  image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSdI7omBFtTyblGgA57jh_4ds2GG0hnn9N53oWp2L3xmRJWhBgt9aEUirkLDcwfG12wAieg6JGmRe__GxVzNzoEC1ezE2jSylgR8NMLyM3LqPpET7sqoaxvvzkFpxYrVFwbAO1873w88c/s1600/P1010424.JPG"
  alt: "Image d'illustration"
---


### Interface télécommande RC en Joystick USB

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSdI7omBFtTyblGgA57jh_4ds2GG0hnn9N53oWp2L3xmRJWhBgt9aEUirkLDcwfG12wAieg6JGmRe__GxVzNzoEC1ezE2jSylgR8NMLyM3LqPpET7sqoaxvvzkFpxYrVFwbAO1873w88c/s200/P1010424.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSdI7omBFtTyblGgA57jh_4ds2GG0hnn9N53oWp2L3xmRJWhBgt9aEUirkLDcwfG12wAieg6JGmRe__GxVzNzoEC1ezE2jSylgR8NMLyM3LqPpET7sqoaxvvzkFpxYrVFwbAO1873w88c/s1600/P1010424.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhDdCOUMc_2sDrI7B8qgv2vPyGIE01acbJWtdj-Zo4zuhdz-b_ZFLDP0W8AOJFOrkivfK9qcN2cRb90dNH5PBAjSESigmE7eWoycIvsSQ9fHDn7Fbyu2XfhPuRLE_5Z17XHtFuCpS5Hwhs/s200/P1010400.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhDdCOUMc_2sDrI7B8qgv2vPyGIE01acbJWtdj-Zo4zuhdz-b_ZFLDP0W8AOJFOrkivfK9qcN2cRb90dNH5PBAjSESigmE7eWoycIvsSQ9fHDn7Fbyu2XfhPuRLE_5Z17XHtFuCpS5Hwhs/s1600/P1010400.JPG)

L'idée de ce projet est de pouvoir **adapter n'importe quelle télécommande de modélisme sur un ordinateur** par le biais du port **USB**. Côté ordinateur, rien d'extraordinaire, on veut simplement obtenir un nouveau **périphérique de type joystick**. Dans mon projet j'utilise une télécommande 4 voies, de ce fait l'adaptateur va "faire croire" (émuler) à l'ordinateur la présence d'un joystick USB 4 axes. La particularité de l'adaptateur vient du fait qu'au lieux d'utiliser la prise écolage sur la télécommande, nous utilisons simplement le récepteur de la télécommande (ou un récepteur compatible à la même fréquence). Ce sont donc les signaux reçus par le récepteur qui seront traités par l'adaptateur. Ce procédé à un avantage incontestable qui est celui de vous offrir la possibilité de vous servir de votre télécommande (sans fils) pour piloter un modèle dans FMS ou votre simulateur ou jeu favoris.

  
**Montage électronique**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiijwfMcNjeHLqIACyZpjmHSEjCFsJTlXPz0K2jzUvgmgeZKpI2nkLWZ6xvYpZrkC0mxgx8jHknjoo3CnvulOeLNkk3mKMFgOl0Kb3dC7sJ_GYFajcIry9hyphenhyphent7mOWf9niXtLRspFdHwy3o/s200/P1010403.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiijwfMcNjeHLqIACyZpjmHSEjCFsJTlXPz0K2jzUvgmgeZKpI2nkLWZ6xvYpZrkC0mxgx8jHknjoo3CnvulOeLNkk3mKMFgOl0Kb3dC7sJ_GYFajcIry9hyphenhyphent7mOWf9niXtLRspFdHwy3o/s1600/P1010403.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi65S155z6Q3MMkDklgHbaiZugRGvU8SQT2ovT4kaELhcQhvAu9k_C8wMCvvjc3Gg_H5FOlJhNExfvtvb7-0A0QbV49LH6bgLaYH2dETESAcRCpKg2b5Z3eRD1viSLr38Cav1ik8-qDPp8/s200/P1010409.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi65S155z6Q3MMkDklgHbaiZugRGvU8SQT2ovT4kaELhcQhvAu9k_C8wMCvvjc3Gg_H5FOlJhNExfvtvb7-0A0QbV49LH6bgLaYH2dETESAcRCpKg2b5Z3eRD1viSLr38Cav1ik8-qDPp8/s1600/P1010409.JPG)

La partie électronique du montage se limite à un seul composant principal: le teensy2++ (équivalent de l'arduino). Ce circuit se branche en USB au pc, et nous utiliserons quatre entrées digitale pour lire les quartes canaux du récepteur de votre télécommande. Le port USB fournit bien assez d'énergie pour alimenter votre récepteur de télécommande. Ceci est très pratique car vous n'avez donc pas a brancher quelque alimentation que ce soit sur votre récepteur.  
  
Une petite astuce pour assurer la connexion  entre le montage et le récepteur consiste à utiliser la connectique des boitiers de PC. En effet dans une tour de pc les boutons et les LEDs de façade se connectent à la carte mère et ces mêmes connecteurs sont parfaitement compatibles avec les pins de votre récepteur. Évidement si vous avez un boitier plastique autour de votre récepteur qui vous impose le détrompeur vous pouvez toujours limer les anges des connecteurs improvisés.

  
  
**Le programme informatique**  
  
Le programme pour arduino est très simple. Le framework arduino fournit une classe permettant d'utiliser le circuit en tant que joystick. Pour envoyer la position des axes du joystick à l'ordinateur on utilise l'objet Joystick qui comporte plusieurs setters X Y Z et Zrotate. Il suffit d'envoyer un entier compris entre 0 et 1023 représentant la position du joystick. Notez que le neutre correspond a la valeur 512.  
Pour lire les canaux du récepteur j'ai choisi de coder une classe nommée ServoRead. On créera un objet de cette classe par canal. Le contructeur de l'objet prend en paramètre le numéro de pin de l'arduino (teensy++ dans mon cas).  
  
Fichier interfaceRC.ino  

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

  int ch1;
  int ch2;  
  int ch3;  
  int ch4;
  
  long lastTime = millis();
  
  while ((millis() - lastTime) < 50) {
    ch1 = Sr1.checkPosition();
    ch2 = Sr2.checkPosition();
    ch3 = Sr3.checkPosition();  
    ch4 = Sr4.checkPosition();
  }
  
  if (use_seconde_pulse) {
    ch1 = Sr1.getPositionB();
    ch2 = Sr2.getPositionB();
    ch3 = Sr3.getPositionB();  
    ch4 = Sr4.getPositionB();  
  }
  
  Joystick.X(ch1);       
  Joystick.Y(ch2);       
  Joystick.Z(ch3);
  Joystick.Zrotate(ch4);
  
}
```
  
```cpp
Fichier ServoRead.h  

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
        long getPositionB();
        
        
  private:
        int _previousState;
        int _pin;
 long _lastTime;
        long _duration;
        long _position;
        long _positionB;
        
};

#endif
```
  
  
Fichier ServoRead.cpp

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
      _positionB = _position;
      _position = map(_duration, 1000, 2000, 0,1023);
      
      //_position = _duration;
      
      
    }
    return _position;
}


long ServoRead::getPosition() {
   return _position; 
  
}

long ServoRead::getPositionB() {
   return _position; 
  
}
```
  
  
**Utilisation côté ordinateur**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7SObnVo_PCZFJzf6Sp2v8O6OCO5yjS6bA_FdMlUOk4tBC_CUNAMyq2p4CZWTD7PPQgVPSW5KtsbUOaAuoW7lOngN2F7pgVUVmq6la7pfx-98QMP28gFAWsnp7Cde8ZqIRbIo_xGUUVEE/s200/fms.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7SObnVo_PCZFJzf6Sp2v8O6OCO5yjS6bA_FdMlUOk4tBC_CUNAMyq2p4CZWTD7PPQgVPSW5KtsbUOaAuoW7lOngN2F7pgVUVmq6la7pfx-98QMP28gFAWsnp7Cde8ZqIRbIo_xGUUVEE/s1600/fms.jpg)

Dans l'absolut le montage est complètement compatible avec tous les systèmes d'exploitation étant donné que l'arduino se comporte comme un joystick standard. De ce fait pour tester l'interface il vous suffit d'utiliser un petit logiciel de configuration de joystick sous linux tel que QJoyPad, sous windows la configuration du joystick peut se faire avec les outils proposés par défaut (dans les propriétés du périphérique). Une fois que l'on s'est assuré que l'interface est opérationnelle, on peut l'utiliser avec [FMS](http://fms.modelisme.com/) par exemple (excellent simulateur de vol de modèles réduits). Le joystick fonctionnera évidement avec tous les jeux ou logiciel supportant le joystick comme périphérique.  
  
  
  
  
**Quelques photos du projet en fonctionnement**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlpAm4brVADQKbQpnMEeSsY_JeivPvoyw90hpdE1Kyl1HvHdFpl9LBZtQFP2pkioDwV4DAefVBiI2aD4vBzgrN9xHVUDsDF8TGzrm0gcwKW0cv29B0Sadn4vqV1bfkWlI2Aa_zwBvMkp8/s200/P1010413.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlpAm4brVADQKbQpnMEeSsY_JeivPvoyw90hpdE1Kyl1HvHdFpl9LBZtQFP2pkioDwV4DAefVBiI2aD4vBzgrN9xHVUDsDF8TGzrm0gcwKW0cv29B0Sadn4vqV1bfkWlI2Aa_zwBvMkp8/s1600/P1010413.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiyUwGVTZNaVZjEAJGwfy0zYI9fR2nkcRBtpbzjIcw9Eve7iiSKdSnfO6t0y9SEecWAY8lTFgKLAIjmsrvhAA7Hv64eD9gSNhMxuJWwRSu8gZTqhhYTc9z6PdwUCKlGEzR65sEjejkh1A8/s200/P1010414.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiyUwGVTZNaVZjEAJGwfy0zYI9fR2nkcRBtpbzjIcw9Eve7iiSKdSnfO6t0y9SEecWAY8lTFgKLAIjmsrvhAA7Hv64eD9gSNhMxuJWwRSu8gZTqhhYTc9z6PdwUCKlGEzR65sEjejkh1A8/s1600/P1010414.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj5nEkWbR_DMfCbgb8ljx4q1Z_zBP3D7IK9Ta4dJjGGFSs_19T3C-YG2QNp7Wd0P71qnUiEROKBHLz6Gbzg6lkHSkKYtJ7ukXcAMmOIimB4PMbeCf0b6s3M05E0m8m2phcj0g3b_Fi_0uM/s200/P1010415.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj5nEkWbR_DMfCbgb8ljx4q1Z_zBP3D7IK9Ta4dJjGGFSs_19T3C-YG2QNp7Wd0P71qnUiEROKBHLz6Gbzg6lkHSkKYtJ7ukXcAMmOIimB4PMbeCf0b6s3M05E0m8m2phcj0g3b_Fi_0uM/s1600/P1010415.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyWteoWYZZMafxfR6iZxZ-20S0-LYl_6VYyLOw11gIaChsPNaA26uN7Cf7SE-1QWjlXm1EiVNjX2ROgMwkOfmW-9uCRJM9cxSFc1p2iRM4YKqWJ108GJfgfali9Xd6paZ-RBWNkwhMuhs/s200/P1010416.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyWteoWYZZMafxfR6iZxZ-20S0-LYl_6VYyLOw11gIaChsPNaA26uN7Cf7SE-1QWjlXm1EiVNjX2ROgMwkOfmW-9uCRJM9cxSFc1p2iRM4YKqWJ108GJfgfali9Xd6paZ-RBWNkwhMuhs/s1600/P1010416.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrxmHYxHV02CcGAMPpFuPbqtLjFESTk9EIou2VmASEOiAhNha-fB1WaQJ0XpQSpsrX4pl8GH317jL-ag2a1NDWKwxNTswlg8AyddorpyNQO2QX2_Z2tb1pIB2oWw7SL_XKUtHudgdMSU4/s200/P1010417.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrxmHYxHV02CcGAMPpFuPbqtLjFESTk9EIou2VmASEOiAhNha-fB1WaQJ0XpQSpsrX4pl8GH317jL-ag2a1NDWKwxNTswlg8AyddorpyNQO2QX2_Z2tb1pIB2oWw7SL_XKUtHudgdMSU4/s1600/P1010417.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6L1NGUXt5GPIw2-V_y7SgnnpL7XSc70eSfDgm03eVWBc3M30rvIvfLtWqfDOoOp0QcVwyOEED6juA8g8j8gLxWFQKVhNLL2sGVB70BUC6H7VZ3YGeHn031zFaInXzV_ZEQIN7Rq_QiMA/s200/P1010418.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6L1NGUXt5GPIw2-V_y7SgnnpL7XSc70eSfDgm03eVWBc3M30rvIvfLtWqfDOoOp0QcVwyOEED6juA8g8j8gLxWFQKVhNLL2sGVB70BUC6H7VZ3YGeHn031zFaInXzV_ZEQIN7Rq_QiMA/s1600/P1010418.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBMd8136q3kMyhUHDPs7AO60aRHz0X-74nEU6TXamGDbuvfPB0gCczbTw8sKNOFA0m56QC2TMPJW-tb6HTlDJl5uYwRdGXKbcbbhdtoQFwmo6AsbFjvCywMelk2KXF7vZtQZp4l9kVnt4/s200/P1010419.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBMd8136q3kMyhUHDPs7AO60aRHz0X-74nEU6TXamGDbuvfPB0gCczbTw8sKNOFA0m56QC2TMPJW-tb6HTlDJl5uYwRdGXKbcbbhdtoQFwmo6AsbFjvCywMelk2KXF7vZtQZp4l9kVnt4/s1600/P1010419.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiepEOTKcUOgtUdv2VIpeSbDRgUXtxdJDHB1K2pUQoR7Mq-SnYSklN415mzXCQccqjOUf4O_F_M-rScZbbJtO4qDhNfWDtBT0Ji3k20MNKBbUKrekCoBQJQvM7eioJb7G8zoMg8OfkYn8E/s200/P1010420.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiepEOTKcUOgtUdv2VIpeSbDRgUXtxdJDHB1K2pUQoR7Mq-SnYSklN415mzXCQccqjOUf4O_F_M-rScZbbJtO4qDhNfWDtBT0Ji3k20MNKBbUKrekCoBQJQvM7eioJb7G8zoMg8OfkYn8E/s1600/P1010420.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgsFZxQaF2t_Dknv2UMn5Q2pevAK2nHLQQ8M1Q0Afk9Yn87NjkVuB1A3WS-IQTm5Hmytou3FboB8fG0BGVlGSsQ7U6GFh1kQMDxiyncp6BiQRdksny7lENx7iAwibR9PbnuC2s8XKTLQLk/s200/P1010421.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgsFZxQaF2t_Dknv2UMn5Q2pevAK2nHLQQ8M1Q0Afk9Yn87NjkVuB1A3WS-IQTm5Hmytou3FboB8fG0BGVlGSsQ7U6GFh1kQMDxiyncp6BiQRdksny7lENx7iAwibR9PbnuC2s8XKTLQLk/s1600/P1010421.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgCpFmd1Fm_uEWxSfJKMGPVbX4K6BhxCeKekSHNZMOLGsK6In-T5k_mp-1s-2VumZRe_7ktk4geuoNfuy4igXK2EbbMQEoe-TjA22aSyEbmJoDx1e_GMLOj0cX9aCYs4kcie5uvOsZXHgY/s200/P1010423.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgCpFmd1Fm_uEWxSfJKMGPVbX4K6BhxCeKekSHNZMOLGsK6In-T5k_mp-1s-2VumZRe_7ktk4geuoNfuy4igXK2EbbMQEoe-TjA22aSyEbmJoDx1e_GMLOj0cX9aCYs4kcie5uvOsZXHgY/s1600/P1010423.JPG)  

  
**Quelques photos du projet**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhDdCOUMc_2sDrI7B8qgv2vPyGIE01acbJWtdj-Zo4zuhdz-b_ZFLDP0W8AOJFOrkivfK9qcN2cRb90dNH5PBAjSESigmE7eWoycIvsSQ9fHDn7Fbyu2XfhPuRLE_5Z17XHtFuCpS5Hwhs/s200/P1010400.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhDdCOUMc_2sDrI7B8qgv2vPyGIE01acbJWtdj-Zo4zuhdz-b_ZFLDP0W8AOJFOrkivfK9qcN2cRb90dNH5PBAjSESigmE7eWoycIvsSQ9fHDn7Fbyu2XfhPuRLE_5Z17XHtFuCpS5Hwhs/s1600/P1010400.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXDXktXcImVrUYe0SVWxr-UihKEq6nGW-6QZBpqpMteJWtDvAIu4QzHNehvrQAB0QBccS37iY4nvC9lhnKN3OpxRo97XhVh7wDl3EBgXVLtexwZndfRa0gcFJjcm2UcvSqe_2E2QAE_gA/s200/P1010401.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXDXktXcImVrUYe0SVWxr-UihKEq6nGW-6QZBpqpMteJWtDvAIu4QzHNehvrQAB0QBccS37iY4nvC9lhnKN3OpxRo97XhVh7wDl3EBgXVLtexwZndfRa0gcFJjcm2UcvSqe_2E2QAE_gA/s1600/P1010401.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMTuX0tICh43FTOneWFGd5JrM_y0xCfD-MfFiwRbO4kn1mqU3EitTN87IYD_8ciTila77H-rzdbclyPHoYKtLH6AZ_IDRr06MsxGiXRXxrSHlf25s0HMSENNgQtFEGN8xJnQ48eKeg7tU/s200/P1010402.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMTuX0tICh43FTOneWFGd5JrM_y0xCfD-MfFiwRbO4kn1mqU3EitTN87IYD_8ciTila77H-rzdbclyPHoYKtLH6AZ_IDRr06MsxGiXRXxrSHlf25s0HMSENNgQtFEGN8xJnQ48eKeg7tU/s1600/P1010402.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiijwfMcNjeHLqIACyZpjmHSEjCFsJTlXPz0K2jzUvgmgeZKpI2nkLWZ6xvYpZrkC0mxgx8jHknjoo3CnvulOeLNkk3mKMFgOl0Kb3dC7sJ_GYFajcIry9hyphenhyphent7mOWf9niXtLRspFdHwy3o/s200/P1010403.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiijwfMcNjeHLqIACyZpjmHSEjCFsJTlXPz0K2jzUvgmgeZKpI2nkLWZ6xvYpZrkC0mxgx8jHknjoo3CnvulOeLNkk3mKMFgOl0Kb3dC7sJ_GYFajcIry9hyphenhyphent7mOWf9niXtLRspFdHwy3o/s1600/P1010403.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeaXcvwrdojjaGwwF1k3KgsJLvffVDMRoEgc_IeGgvYbG5nuh6TMaZpBWe5yn2sytTj8_xkMtFyVAThYG88tVD725SHxS5AAtxOqUw0LsoRjVh01Bv1Vox-7DEgHAUxYIcg9nIsOk6RYc/s200/P1010404.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeaXcvwrdojjaGwwF1k3KgsJLvffVDMRoEgc_IeGgvYbG5nuh6TMaZpBWe5yn2sytTj8_xkMtFyVAThYG88tVD725SHxS5AAtxOqUw0LsoRjVh01Bv1Vox-7DEgHAUxYIcg9nIsOk6RYc/s1600/P1010404.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiETp5kHk0jVn7HQkuiefXHLvlo-9AFmaMHOa3iUAE4mkcykb_BXoV3cygSjNL-fAJNUtJ6jfYTf2h-fLOJJjuaDQU_5h453zLoCx3zATWF-JxiNem5sPkcgCieje1kXzmoSW-iz9KqNQw/s200/P1010405.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiETp5kHk0jVn7HQkuiefXHLvlo-9AFmaMHOa3iUAE4mkcykb_BXoV3cygSjNL-fAJNUtJ6jfYTf2h-fLOJJjuaDQU_5h453zLoCx3zATWF-JxiNem5sPkcgCieje1kXzmoSW-iz9KqNQw/s1600/P1010405.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3N4Dh-VO9EZOwWud3EKHumC67pUraGmLZgiNQcZ-65k09viiK05ITg0601wVGa5iYYTfUHGAG2vGuiGF15c8qJki3yhRU1dLkBDtS6x8HiGVsN1sNW-QsYxL4IriZBFjaMDq4fBWDSGE/s200/P1010406.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3N4Dh-VO9EZOwWud3EKHumC67pUraGmLZgiNQcZ-65k09viiK05ITg0601wVGa5iYYTfUHGAG2vGuiGF15c8qJki3yhRU1dLkBDtS6x8HiGVsN1sNW-QsYxL4IriZBFjaMDq4fBWDSGE/s1600/P1010406.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi65S155z6Q3MMkDklgHbaiZugRGvU8SQT2ovT4kaELhcQhvAu9k_C8wMCvvjc3Gg_H5FOlJhNExfvtvb7-0A0QbV49LH6bgLaYH2dETESAcRCpKg2b5Z3eRD1viSLr38Cav1ik8-qDPp8/s200/P1010409.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi65S155z6Q3MMkDklgHbaiZugRGvU8SQT2ovT4kaELhcQhvAu9k_C8wMCvvjc3Gg_H5FOlJhNExfvtvb7-0A0QbV49LH6bgLaYH2dETESAcRCpKg2b5Z3eRD1viSLr38Cav1ik8-qDPp8/s1600/P1010409.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhye-DdnTeSzAKDJN5TCQ3BGPkh9JmRz4hyU5_O08zzdnAFpNlMkBJXH13ZGMf7-rrE-Th89sR7SQD__Z0sQczudiG9aQB5oS813l0FbdrqcCmbsmbHMM8npLt26zT-qBXoEXngBf425E0/s200/P1010410.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhye-DdnTeSzAKDJN5TCQ3BGPkh9JmRz4hyU5_O08zzdnAFpNlMkBJXH13ZGMf7-rrE-Th89sR7SQD__Z0sQczudiG9aQB5oS813l0FbdrqcCmbsmbHMM8npLt26zT-qBXoEXngBf425E0/s1600/P1010410.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIsCcB8eEX9VEpCIKtxAVQaTreQ4badknekuvQM0b_x5yQTwmga6yPMm-LdauFfNsZyOTqdvzeKsXoGIuhA0PNvTUeoNMIwsXx_RYLuFQg67cniAprVvhYIA4UTZTdqQsUwZyvrdHbKZg/s200/P1010412.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIsCcB8eEX9VEpCIKtxAVQaTreQ4badknekuvQM0b_x5yQTwmga6yPMm-LdauFfNsZyOTqdvzeKsXoGIuhA0PNvTUeoNMIwsXx_RYLuFQg67cniAprVvhYIA4UTZTdqQsUwZyvrdHbKZg/s1600/P1010412.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSdI7omBFtTyblGgA57jh_4ds2GG0hnn9N53oWp2L3xmRJWhBgt9aEUirkLDcwfG12wAieg6JGmRe__GxVzNzoEC1ezE2jSylgR8NMLyM3LqPpET7sqoaxvvzkFpxYrVFwbAO1873w88c/s200/P1010424.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSdI7omBFtTyblGgA57jh_4ds2GG0hnn9N53oWp2L3xmRJWhBgt9aEUirkLDcwfG12wAieg6JGmRe__GxVzNzoEC1ezE2jSylgR8NMLyM3LqPpET7sqoaxvvzkFpxYrVFwbAO1873w88c/s1600/P1010424.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj4eMCBMCzyRumOkIBGsuh-XJ0PN2bBgoo4CfU4F_EDcJpO8cojYbZM1zh3rS5U0X5vH8o9UazAfKSwYYTEAngMkffxHYqOHaQTrF0rg_5ZCPDTqMDgodhtHQ28LtIvFSj3w4xBqcb4rPs/s200/P1010425.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj4eMCBMCzyRumOkIBGsuh-XJ0PN2bBgoo4CfU4F_EDcJpO8cojYbZM1zh3rS5U0X5vH8o9UazAfKSwYYTEAngMkffxHYqOHaQTrF0rg_5ZCPDTqMDgodhtHQ28LtIvFSj3w4xBqcb4rPs/s1600/P1010425.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjBJOkoV8thf7D9G9Ncx76536DFLYZCMvHwEk6vVDnN7wdLMj3fVjsNcda0BfWdVTjYP65C3fSuPhhQbzr3oQIvUdhY3x-4jCxpT3nbiBDiwj_AVezseJZSI3iSaO-8TprP9xYascsEg3Q/s200/P1010426.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjBJOkoV8thf7D9G9Ncx76536DFLYZCMvHwEk6vVDnN7wdLMj3fVjsNcda0BfWdVTjYP65C3fSuPhhQbzr3oQIvUdhY3x-4jCxpT3nbiBDiwj_AVezseJZSI3iSaO-8TprP9xYascsEg3Q/s1600/P1010426.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjpyl6PIzuFs7YQHwojHR9_cVEkFrn1yDS2Q7jfiQPs5OMyPO0FLQs-sIZwHiCXVX8cERyFj6wGWCqohVPPxPkYYG7juvCtT8wukimUJl5gtfuoj7Whx0AZgRRWMa6YXT_6pcuixni04UQ/s200/P1010428.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjpyl6PIzuFs7YQHwojHR9_cVEkFrn1yDS2Q7jfiQPs5OMyPO0FLQs-sIZwHiCXVX8cERyFj6wGWCqohVPPxPkYYG7juvCtT8wukimUJl5gtfuoj7Whx0AZgRRWMa6YXT_6pcuixni04UQ/s1600/P1010428.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh2OxD_aTOScGASifQjBP4z3z0dbLHHMC-PgZsqq6vehN80ZJoK7dNfkmIQnkOWsi6QZcUXMc1J_HAASOmjy3c9RTQfDr9yHutTsNIp5ItfuTeuJTMCamlpmU22tr_3ltNRoDdASHMhg54/s200/P1010429.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh2OxD_aTOScGASifQjBP4z3z0dbLHHMC-PgZsqq6vehN80ZJoK7dNfkmIQnkOWsi6QZcUXMc1J_HAASOmjy3c9RTQfDr9yHutTsNIp5ItfuTeuJTMCamlpmU22tr_3ltNRoDdASHMhg54/s1600/P1010429.JPG)


**Documents annexes**  
  
[Télécharger les sources complètes du projet](http://artiom21.free.fr/projets/arduino-telecommande-rc-usb/interfaceRC.zip)