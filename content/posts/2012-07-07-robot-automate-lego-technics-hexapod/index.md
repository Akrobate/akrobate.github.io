---
date: '2012-07-07T14:05:20+02:00'
draft: false
title: "Robot automate Lego Technics Hexapod"
slug: "robot-automate-lego-technics-hexapod"
tags:
  - automate
  - lego
  - robot
  - robotique
categories:
  - Robotique
cover:
  image: P1010101.avif
  alt: Image d'illustration
ShowToc: true
description: Concevez un robot automate Lego Technic à 6 pattes ! Apprenez à créer des portes logiques pneumatiques avec des vérins pour programmer ses mouvements.

---


![Robot lego hexapode](P1010101.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![Robot lego hexapode pneumatique](P1010100.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

L'idée principale de ce projet est de **réaliser un automate** avec les pièces de legos pneumatiques. En effet parmi les pièces lego techniques standards on a toute une mécanique pneumatique fournie. Ces pièces sont les vérins, pompes à air, tuyauterie, et interrupteurs pneumatiques. C'est en utilisant une astuce consistant a monter les interrupteurs pneumatiques sur les vérins que l'on peut concevoir des "**portes logiques**" qui vont nous permettre de "coder" des séquences de mouvement. D'ailleurs des séquences bien plus complexes peuvent être conçues avec des pièces de légo pneumatique et simplement mécanique. Par exemple célébrer le centenaire du pionnier de l'informatique Alan Turing, huit étudiants en master de l'Ecole normale supérieure de Lyon ont fabriqué une sorte d'ordinateur en Lego. ([article du Monde sur cette réalisation](http://www.lemonde.fr/sciences/article/2012/06/22/l-ordinateur-en-lego-inspire-par-alan-turing_1723058_1650684.html))


## Le châssis du robot hexapode

Le châssis est réalisé en legos techniques avec des pièces très courantes. Le robot est un hexapode et possède donc six pattes. Le lien entre les pattes est réalisé en fonction des nécessites de la séquence de déplacement. Les pattes extérieures sont reliés entre elles de manière a ce que lorsque la patte avant gauche avance, la patte arrière gauche avance aussi. Ce procédé est reproduit évidement sur le coté droit. Les deux pattes de milieux sont solidaire dans le mouvement. Lorsque la patte de milieu gauche monte, la matte de milieu à droite descend. On peut donc réduire (factoriser) les pattes en trois sous ensembles. Les pattes avant et arrière gauches, les pattes avant et arrière droite, et les pattes de milieu. On aura donc besoin de trois contrôles distincts pour contrôler le châssis. Le contrôle des pattes du milieu doit être plus puissant que les autres étant donné que ce sont ces pattes là qui soulèvent un coté du robot puis l'autre. J'ai choisis d'installer deux vérins fonctionnant de manière solidaire, et étant montés en parallèle entre eux pour contrôler les pattes de milieu. Le côté gauche et le côté droit ont un vérin chacun comme moteur.  


{{% gallery %}}

![](P1010073.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010074.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010075.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010077.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010078.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010079.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010080.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010081.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010082.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010083.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010084.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010085.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010087.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010088.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010089.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Installation des interrupteurs pneumatiques

![](P1010103.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](P1010104.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Sur la base du châssis on monte ensuite l'ensemble des interrupteurs qui vont déclencher les séquences de chaque ensemble de pattes. Pour rappel nous avons donc trois sous ensembles a contrôler, de ce fait il nous faudra trois interrupteurs actionné par un des trois sous ensembles. Cela revient en quelque sorte a faire contrôler un interrupteur par l'action d'un vérin. De ce fait l'ensemble interrupteur et vérin donne un genre d'équivalent au servomoteur (dans le sens où on a un retour sur la position du vérin).

Les interrupteurs sont tous les 3 alimentés en air comprimé de simultanément. Il faudra donc deux T pour obtenir 3 sorties de pression depuis la pompe.


## Séquence de déplacement
  
Maintenant que nous avons notre ensemble de 3 sous ensembles à contrôler et 3 interrupteurs montés sur les vérins, nous pouvons nous attaquer à la partie câblage de la tuyauterie. C'est ce fameux câblage qui va permettre de créer la séquence de déplacement. Le principe de déplacement que l'on souhaite obtenir est très simple. On pourrait le résumer en ces quelques points:  
  

 1. Monter le coté droit du robot (en actionnant les deux vérins de milieu montés en parallèle)
 2. Avancer les pattes de droite et (simultanément ou pas) reculer les pattes de gauche.
 3. Descendre le coté droit, et donc obligatoirement le coté gauche monte
 4. Reculer les pattes de droite et (simultanément ou pas) avancer les pattes de gauche.

  
Cette séquence pourra être codée grâce a la connectique des tuyaux sur les 3 vérins (je dis 3 car je considère les 2 vérins du milieu comme un seul étant donné qu'ils sont montés en parallèle entre eux grâce a deux T ) et les 3 interrupteurs. Pour que ce soit plus simple a visualiser appelons les 3 ensembles de vérins à contrôler V1, V2, V3. et les 3 interrupteurs I1, I2, I3. Le V1 c'est le vérin de gauche contrôlant les 2 pattes avant et droite de gauche, le V2 c'est le vérin de droite et enfin le V3 c'est les deux vérins montés en parallèle et s'occupant de soulever le coté gauche et le coté droit du robot (pattes de milieu). Les vérins V1, V2, V3 activent respectivement les interrupteurs I1, I2, I3. L'idée du montage de la tuyauterie c'est de faire en sorte que l'interrupteur In contrôle le vérin V(n-1) et est activé par le vérin Vn. En gros I3 doit contrôler V2, I2 doit contrôler V1 et le I1 doit contrôler V3. Comme vous pouvez le voir cela donne une boucle au final.  
  
Vous aurez sans doute besoin de corriger les sens de déplacement des vérins. Le plus simple reste de déterminer ces sens par la pratique. Selon le sens de la connexion de chaque vérin sur chaque interrupteur, le mouvement général peut être modifié. Exemple le robot peut tourner sur lui même au lieu d'avance en ligne droite.  
  
  
## Photos  du robot Hexapode en légo Technics

{{% gallery %}}

![](P1010091.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010093.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010094.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010099.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010100.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010102.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010103.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010104.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010105.avif)
{ mode="lightbox" miniature-width=200 }

![](P1010106.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}
