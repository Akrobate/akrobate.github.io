---
date: '2026-09-25T14:05:20+02:00'
draft: false
title: "Télécommande infrarouge lego power function et librairie arduino"
slug: "telecommande"
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
  image: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" # ou un lien externe / paramètre perso
  alt: "Image d'illustration"
---


## Test zone



{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="25%" >}}

{{< image-right src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="25%" >}}


 Les légos power functions sont devenu assez courants dans des lots de taille considérable de lego technics. Les power functions se composent d'un moteur assez gros pour la motorisation généralement, d'un moteur de taille moyenne généralement pour contrôler des bras ou autres, d'un récepteur infrarouge d'un pack d'alimentation et de l'émetteur infrarouge. Chaque récepteur comporte deux connecteurs pour des moteurs et possède un switch pour régler le canal sur lequel il doit attendre les commandes. Chaque émetteur infrarouge comporte évidement la fonction de sélection de canal pour déterminer sur quel canal émettre.  

---

{{< figure 
    src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG"
    alt="Mon image"
    width="150"
    >}}
### Télécommande infrarouge lego power function et librairie arduino

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s200/telecommande+lego+et+recepteur.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG#floatleft)

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV7P0lvB0iiqHxY_V4NE6z07Z0GxIeDuWAO9OxO40kYTDIPr6N1_t0ToGUOgzx06p4jNoXq7Iq6bL7o6DKOINYql8lXXsfbSA39J_dWu7XiHh4wGeAlpIn0mdfM8ipf8ekP60Z3bU0g6w/s200/telecommande+lego+et+power+functions.JPG#floatleft)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiV7P0lvB0iiqHxY_V4NE6z07Z0GxIeDuWAO9OxO40kYTDIPr6N1_t0ToGUOgzx06p4jNoXq7Iq6bL7o6DKOINYql8lXXsfbSA39J_dWu7XiHh4wGeAlpIn0mdfM8ipf8ekP60Z3bU0g6w/s1600/telecommande+lego+et+power+functions.JPG#floatleft)Un chassis motorisé de légo technic est souvent très pratique pour réaliser une base pour un robot. L'idée de cet article est de vous présenter une librairie pour arduino qui permet de **commander le récepteur infrarouge des legos technics power functions**. Le principe de l'interface est d'émuler les signaux de la télécommande. En effet le protocole lego n'est pas très complexe, et surtout il ouvre la possibilité d'adresser le récépteur légo différemment et donc d'accéder  a de nouvelles fonctionnalités tels que la **vitesse de rotation** de chaque moteur (sur **7 niveaux**) et la **fonction de frein** qui permet d'immobiliser l'axe du moteur. Pour mettre en exemple cette librairie je vous propose de réaliser une télécommande améliorée pour lego technics power function.  


  
  
  
**Lego Power Functions récepteur**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjewL09Mg8zDe2GuOFGEmT48u0i-E9UuyFEefgcHSgo3cQ_Tzm6Sjkv7cp5b9IS3cYr9JokYTwmoy0mZfTpxEH0tCXCUEUY82m1QSrTDRnDdzJreKx2hbo4dfuW9nwJsm0CcM5t-HQE5cU/s200/lego+power+functions.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjewL09Mg8zDe2GuOFGEmT48u0i-E9UuyFEefgcHSgo3cQ_Tzm6Sjkv7cp5b9IS3cYr9JokYTwmoy0mZfTpxEH0tCXCUEUY82m1QSrTDRnDdzJreKx2hbo4dfuW9nwJsm0CcM5t-HQE5cU/s1600/lego+power+functions.JPG)

 Les légos power functions sont devenu assez courants dans des lots de taille considérable de lego technics. Les power functions se composent d'un moteur assez gros pour la motorisation généralement, d'un moteur de taille moyenne généralement pour contrôler des bras ou autres, d'un récepteur infrarouge d'un pack d'alimentation et de l'émetteur infrarouge. Chaque récepteur comporte deux connecteurs pour des moteurs et possède un switch pour régler le canal sur lequel il doit attendre les commandes. Chaque émetteur infrarouge comporte évidement la fonction de sélection de canal pour déterminer sur quel canal émettre.  
  
  
  
**Télécommande améliorée à base d'arduino**  
  
La télécommande que je vous présente ici est très simple. Son cout global n'excède pas une trentaine d'euros. En effet son composant principal est un teensy2.0++ qui est compatible à 100% avec l'IDE arduino.  
La télécommande comporte 8 boutons en tout. 4 boutons pour chaque moteur. Deux boutons servent a regler la vitesse et changer de sens pour chaque moteur. Un bouton permet d'envoyer un signal de vitesse nulle pour chaque moteur, et enfin un autre bouton permet d'envoyer la commande de frein pour chaque moteur. Cette commande permet d'appliquer une contrainte sur l'axe du moteur à l'arrêt.  
  
  
  

  
  
**Librairie pour arduino LegoRC**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiq-54riKjnFDsre9X0Q-bOXz9I8VHWA7Yer8JgMYmLETWIq-384aQqMR9IrjLaFmIOVTnUZQhWKoz_X055__2JGwTwBNa4CIIe_1cFetYWOjMffRdoamQaIfXQf0oe_ZPLdwXn329jSds/s200/telecommande+et+recepteur+lego+pf.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiq-54riKjnFDsre9X0Q-bOXz9I8VHWA7Yer8JgMYmLETWIq-384aQqMR9IrjLaFmIOVTnUZQhWKoz_X055__2JGwTwBNa4CIIe_1cFetYWOjMffRdoamQaIfXQf0oe_ZPLdwXn329jSds/s1600/telecommande+et+recepteur+lego+pf.JPG)

Le code source permettant de communiquer avec le récepteur légo est une classe. Le constructeur de cette classe prend en paramètre la broche sur laquelle vous avez branché la diode infrarouge. On utilisera que trois méthodes publiques: sendCommand(int n1, int n2, int n3), sendSignalString(String msg), autoSend(). Chaque signal infrarouge se compose de 3 mots de 4 bits et d'un mot de vérification (checksum des 3 mots). SendCommand vous permet d'envoyer les 3 mots en entiers compris entre 0 et 15. La méthode sendSignalString, vous permet d'envoyer une chaine de caractères contenant les caractères '1' ou '0'. Cette chaine correspond a la concaténation des trois commandes en binaire. Cette chaine devra obligatoirement faire 16 caractères. Vous aurez donc dans ce cas là calculer la valeur du checksum vous mêmes.  
  
  
**Protocole infrarouge, signaux et documentation**  
  
Le protocole utilisé par le récepteur légo est expliqué en détail dans le document: [Lego Power Function RC v120.pdf](http://artiom21.free.fr/projets/arduino-lego-telecommande/LEGO%20Power%20Functions%20RC%20v120.pdf) . En effet dans ce document on comprends rapidement quels commande envoyer pour chaque comportement des moteurs voulus. J'attire votre attention sur le **Combo PWM mode**. Ce mode permet de contrôler les deux moteurs avec une seule commande envoyé. Pour envoyer les commandes au récepteur vous allez pouvoir utiliser la méthode sendCommand de la classe LegoRC. En effet les mots correspondent aux "nibble" de la documentation. Donc le premier mot sera un mot de configuration. Le deuxième la commande pour le moteur B et le troisième la commande pour le moteur A.  
Vous pouvez explorer ce document qui comporte tous les modes d'adressage supporté par le récepteur. J'ai choisi d'utiliser le Combo PWM mode car ce dernier permet d'avoir le contrôle de la vitesse. En effet chaque moteur a 7 niveaux de vitesse différente pour chaque sens.  
  
  
**Partie électronique de la télécommande**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyyQmwtTpS9VQWiuV15R4uGKMa3kjJVUwCNWUWrLBSozYBAfbQmLyAN9uc9tPQXyt7aPREFsx9DCLNf1TXsfWJHEKXGdhyEp24ONb_OmRNWwM5SdRWl1AU_Tt-Q9jLowU3yb5fAJHE5Zw/s200/telecommande+lego+electronique.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyyQmwtTpS9VQWiuV15R4uGKMa3kjJVUwCNWUWrLBSozYBAfbQmLyAN9uc9tPQXyt7aPREFsx9DCLNf1TXsfWJHEKXGdhyEp24ONb_OmRNWwM5SdRWl1AU_Tt-Q9jLowU3yb5fAJHE5Zw/s1600/telecommande+lego+electronique.JPG)

Comme dis ci dessus, la partie électronique ne présente vraiment aucune difficulté particulière. En effet tout le travail est assuré par le micro contrôleur Teensy2.0++. J'attire cependant votre attention sur quelques détails. Je vous recommande de ne pas oublier de mettre une résistance sur la led infrarouge. Résistance d'environ 220 Ohm. Par ailleurs pour bien distinguer chaque état des boutons il faut une résistance de rappel a la masse. Il s'agit de connecter la pin d'entrée de l'inter a la masse à travers d'une résistance d'environ 30 kOhm. et le bouton positionnera cette pin au +5V lorsque le bouton est enfoncé. Par ailleurs le ciruit est entièrement auto alimenté par l'USB du teensy. Il ne faudra donc surtout pas oublier de relier les broches GND et +5V du teensy à celles du circuit.  
  
  
  
**Quelques photos**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2uaVevx6oswH7sWfjNYsi4TLz-eLqp0JnE2rwQggh7lnDVDFADa65Eipc0-16MuFC_IIuRBZiU722eMIpDXuhAN0iOzL3gYPK_jJh7U_MfZgYYhNuGWh7ZL4bvJqtpiEBQ5MWt9FEDOQ/s200/P1010057.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2uaVevx6oswH7sWfjNYsi4TLz-eLqp0JnE2rwQggh7lnDVDFADa65Eipc0-16MuFC_IIuRBZiU722eMIpDXuhAN0iOzL3gYPK_jJh7U_MfZgYYhNuGWh7ZL4bvJqtpiEBQ5MWt9FEDOQ/s1600/P1010057.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYrQ242jyrF1shdjTgx6diVX4Tc6CsDMLWoX8t6k0DJIEOrFhdRWKEciEnnxSsKUxSWRTEYU_VWc4O3e6hlVT3r37lWDqjBSHKFjVR4_sNQn4CGn9odTn6aT2lLvB6OnZqtX0UAKiF5cA/s200/P1010058.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYrQ242jyrF1shdjTgx6diVX4Tc6CsDMLWoX8t6k0DJIEOrFhdRWKEciEnnxSsKUxSWRTEYU_VWc4O3e6hlVT3r37lWDqjBSHKFjVR4_sNQn4CGn9odTn6aT2lLvB6OnZqtX0UAKiF5cA/s1600/P1010058.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQQvKG6YSUu6rIM4iUnQm41g3s5mYdTyZpAKh1qWfkzmQgLc58wfhhOWtIsMEu34F-g_0ewvg59o9p_cKJUARu9yES0H1gu8s957Mp5-zCD1H4YjqHcg-MmiTDsJzlhfn86_FNwMcnvYU/s200/P1010059.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQQvKG6YSUu6rIM4iUnQm41g3s5mYdTyZpAKh1qWfkzmQgLc58wfhhOWtIsMEu34F-g_0ewvg59o9p_cKJUARu9yES0H1gu8s957Mp5-zCD1H4YjqHcg-MmiTDsJzlhfn86_FNwMcnvYU/s1600/P1010059.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEig2olRU3GDHboqixzep9bISNmIrJmQBFPJ9yxumzxO7P1Dvy4fQAnYp3KMsslsLgfsmBHc6lsmK8Gwu2hy7zzW38kTmqPxKD1UjzRvlTNupuYudoaSSRxjENvexbJ8u095WGCIMCHxlNA/s200/P1010060.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEig2olRU3GDHboqixzep9bISNmIrJmQBFPJ9yxumzxO7P1Dvy4fQAnYp3KMsslsLgfsmBHc6lsmK8Gwu2hy7zzW38kTmqPxKD1UjzRvlTNupuYudoaSSRxjENvexbJ8u095WGCIMCHxlNA/s1600/P1010060.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinKfdMx5pVtDVejwxZE-aZclwS4arw2OkvpGkCQtgpl0yC8U28Sk7Mj2uEoy-4SdL76fWKRFgdoUD8JolP9dThltDjfOaI99UwRIb-AirN-oZlNvNRbhATk3bJy1-NP101dt9yrbwGdGY/s200/P1010063.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinKfdMx5pVtDVejwxZE-aZclwS4arw2OkvpGkCQtgpl0yC8U28Sk7Mj2uEoy-4SdL76fWKRFgdoUD8JolP9dThltDjfOaI99UwRIb-AirN-oZlNvNRbhATk3bJy1-NP101dt9yrbwGdGY/s1600/P1010063.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEe3nf5j_Irps4h-TfitfmvwoKkIrf_HMMiDhpgOpwehIkETljO1HYjSvAYxCUKGKyJ609_K-bVwfV8jn1IvCbZg9Czhiia1mFBOS8g7CPzgl6iV2gtef6DJ7Ua_qNlZ9XBlQD3AtIoSw/s200/P1010064.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEe3nf5j_Irps4h-TfitfmvwoKkIrf_HMMiDhpgOpwehIkETljO1HYjSvAYxCUKGKyJ609_K-bVwfV8jn1IvCbZg9Czhiia1mFBOS8g7CPzgl6iV2gtef6DJ7Ua_qNlZ9XBlQD3AtIoSw/s1600/P1010064.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi8WeOJ0ubXW6sGkQW1UJkCJCqQUuDVPv1OeWD9xONP6SMpr__PbLtGjpKHHzS-YzChXRzNfNh8Ojw8bDO0hcGxpB72COhFI9tMT8bVtMeH_9lm0E0ChMHGLNKsCP17lNKqVs0yleh4Tyo/s200/P1010065.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi8WeOJ0ubXW6sGkQW1UJkCJCqQUuDVPv1OeWD9xONP6SMpr__PbLtGjpKHHzS-YzChXRzNfNh8Ojw8bDO0hcGxpB72COhFI9tMT8bVtMeH_9lm0E0ChMHGLNKsCP17lNKqVs0yleh4Tyo/s1600/P1010065.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_qZbNnoxRUsX7RuLPWjOLBE6fyj_uwjdloPBXjM_iOVbIhl4YbAxVy9ZhySkE6gblUjxHWZiw_lLOKBIWjjnV9MdDLBav3z2sA3p0WfMvPk8hQwUg1bspv54y3Jb7RNppN8ccdH60BQQ/s200/P1010066.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_qZbNnoxRUsX7RuLPWjOLBE6fyj_uwjdloPBXjM_iOVbIhl4YbAxVy9ZhySkE6gblUjxHWZiw_lLOKBIWjjnV9MdDLBav3z2sA3p0WfMvPk8hQwUg1bspv54y3Jb7RNppN8ccdH60BQQ/s1600/P1010066.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZcAO_LRgnlH3dM2O4iT1W7e2w9851qONn8tq76NE9sQUIlyvOV-T_CvH70HUGO2D6Y7if31feT-2_thM7vGsEhLwzBjIA7tRXIw8Zrqs0EoAbZYWP8Z3bpBhq1FYwguUH09c1W8tS_wY/s200/P1010067.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZcAO_LRgnlH3dM2O4iT1W7e2w9851qONn8tq76NE9sQUIlyvOV-T_CvH70HUGO2D6Y7if31feT-2_thM7vGsEhLwzBjIA7tRXIw8Zrqs0EoAbZYWP8Z3bpBhq1FYwguUH09c1W8tS_wY/s1600/P1010067.JPG)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj_QDz3rZ6GRKqx_ntte-q7wOiuIYqaog2v7XH1FeUjRnAh3f_kvePRum7KP8jZw1AYaQJylDoBXXnb-I6LGyHzlV5g9O3GGIySVxUGI46nxEsj0VDX8xuG4r2-FPx5Bxrs3BxYqLKfpGk/s200/P1010068.JPG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj_QDz3rZ6GRKqx_ntte-q7wOiuIYqaog2v7XH1FeUjRnAh3f_kvePRum7KP8jZw1AYaQJylDoBXXnb-I6LGyHzlV5g9O3GGIySVxUGI46nxEsj0VDX8xuG4r2-FPx5Bxrs3BxYqLKfpGk/s1600/P1010068.JPG)  



## Gallery test

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< image-left src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXPU_J-0HEu1jI0gn31-R7TtRmdVJXghvDvHDQETRU2bdU8jSRnChfS0WeSrDBAr5J2bmjsiSdZj8wypf9b6N9pky_ON632XFFi3C0_x7Q_XxPFpvWw1i0DZtThVjTdIK7MWGcwU1Z5g4/s1600/telecommande+lego+et+recepteur.JPG" alt="Ma photo" width="30%" >}}

{{< clear-float >}}


---






  
**Documents annexes**  
  
[Lego Power Function RC v120.pdf](http://artiom21.free.fr/projets/arduino-lego-telecommande/LEGO%20Power%20Functions%20RC%20v120.pdf)  
[Classe LegoRC pour arduino.zip](http://artiom21.free.fr/projets/arduino-lego-telecommande/Classe%20LegoRC%20pour%20arduino.zip)  
[Programme complet telecommande infrarouge lego pour arduino.zip](http://artiom21.free.fr/projets/arduino-lego-telecommande/Programme%20complet%20telecommande%20infrarouge%20lego%20pour%20arduino.zip)



