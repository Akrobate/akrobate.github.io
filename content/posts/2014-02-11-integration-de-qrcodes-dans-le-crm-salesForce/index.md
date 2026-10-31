---
date: '2014-02-11T14:05:20+02:00'
draft: false
title: Intégration de QRcodes dans le CRM SalesForce
slug: integration-qrcodes-dans-salesforce
tags:
  - apex
  - CRM
  - php
  - QRCode
  - SalesForce
categories:
  - Web
cover:
  image: "Logo-Gimp-2-8.avif"
  alt: "Image d'illustration"
description: pas de descrition
showTOC: true
---

### Intégration de QRcodes dans le CRM SalesForce

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs5AAuF0VtMDpjiMkiflv4apQPeHibmPKctdSMVCdHjGEVRZDdNVj-v1Y9zdFZ67PCALZ8ypMMj3VOjji02qlwJxIDMa0YDuSimUKn9EFT-Y4Sv-AGVzrAyt-VA9ByUnP5tDJ1G4jvuR4/s1600/exemple+d%2527int%25C3%25A9gration+des+qrcodes+dans+salesforce.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs5AAuF0VtMDpjiMkiflv4apQPeHibmPKctdSMVCdHjGEVRZDdNVj-v1Y9zdFZ67PCALZ8ypMMj3VOjji02qlwJxIDMa0YDuSimUKn9EFT-Y4Sv-AGVzrAyt-VA9ByUnP5tDJ1G4jvuR4/s1600/exemple+d%2527int%25C3%25A9gration+des+qrcodes+dans+salesforce.png)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIgy8jGZ3tzizY9N2V6DAEveYFLuf3DiZ4POm2xq2isx9l0n6Pv3GJmkytuSDfNQcaaoC2nAUDUDytwd-5o7Rk-iRUbeyQRda4jEknms5ubS05bKHT1N_J7aM3ktU8KGJcjWSyRWHfhFc/s1600/1.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIgy8jGZ3tzizY9N2V6DAEveYFLuf3DiZ4POm2xq2isx9l0n6Pv3GJmkytuSDfNQcaaoC2nAUDUDytwd-5o7Rk-iRUbeyQRda4jEknms5ubS05bKHT1N_J7aM3ktU8KGJcjWSyRWHfhFc/s1600/1.png)Salesforce est un **cloud CRM  payant** extrêmement populaire en ce moment dans le monde des entreprises. SalesForce promet à ses clients un **logiciel en ligne de gestion de la relation client (CRM) clef en main**, opérationnelle instantanément pour un coût plus tôt acceptable face aux **avantages immédiats de la solution**. En effet la mise en place de  Salesforce ne nécessite pas obligatoirement des connaissances informatiques approfondies. Un manager d'équipe par exemple est tout à fait apte à configurer une instance Salesfoce de manière relativement poussée en ce qui concerne les contraintes métier de l'entreprise. La **solution ne nécessitant aucune infrastructure** au sein de l'organisation beaucoup d'entreprises sont séduites par cette solution. Cependant cette facilité à aussi son **gros inconvénient**: il s'agit de l'**externalisation** de l'ensemble des **données** de la relation client et parfois (souvent) même des données **stratégiques** de l'entreprise.

  
**Dans cet article je vous propose l'intégration d'une nouvelle fonctionnalité** dans votre **Salesforce**: Les [QRCodes](http://fr.wikipedia.org/wiki/Code_QR). Vous allez pouvoir **scanner votre fiche contact** salesfoce **affichée a l'écran** avec votre Smartphone afin que le **contact soit automatiquement ajouté a votre répertoire téléphonique**.  
  
Les QR Codes sont des codes bar en 2 dimensions très populaires en ce moment pour emmagasiner une petite quantité d'informations. Vous trouverez souvent ces codes barres dans la presse pour communiquer des liens par exemple. Les [QRCodes](http://fr.wikipedia.org/wiki/Code_QR) peuvent aussi (entre autres) contenir une carte de visite, qui une fois lue par téléphone proposera l'option d'ajout au répertoire (ou tout autre action associée sur le terminal à ce type d'enregistrement). Les cartes de visites dans les QRCodes sont simplement une chaîne de caractères formatés dans le format de la [VCARD](http://fr.wikipedia.org/wiki/VCard).  
  
  
**QRCodes dans les vues contacts de SalesForce**  
  
Nous allons chercher a **intégrer un QRCode dynamique sur la fiche contact** de SalesForce. Ce **QRCode** reprendra **simplement les informations contenues dans la fiche contact courante**. Afin de réaliser cette prouesse, qui consistera à récuperer les informations de la fiche courante et les transmettre à un script php qui réalisera la génération de l'image contenant le QRCode, nous allons utiliser une technique vieille comme le web - l'intégration de contenus avec une balise IFrame en HTML.  
  
Comme vous l'aurez compris nous allons avoir besoin d'héberger un petit script php qui va réaliser le rendu du QRCode. Ce script peut être hébergé sur n'importe quel hébergement mutualisé grand public. Ce dernier sera simplement chargé de récupérer en paramètres GET les différentes information de la page contact puis de les formater selon une chaîne de caractères connues des téléphones comme la [VCard](http://fr.wikipedia.org/wiki/VCard) puis notre script réalise le rendu en passant par un **petite lib qui genere les QRCodes**.  
  
Voici donc le script de generation des qrcodes.  
  

<?php
 /**
  * Parametres envoyés par l'appel réalisé depuis sales force
  *  Le format : {!contact.Id} correspond au format de templating 
  * Visual pages dans salesforce permettant d'acceder aux proprietés
  * courrantes de la page
  * 
  * Mapping SF
  * 
  * id={!contact.Id}&
  * nom={!contact.LastName}&
  * prenom={!contact.FirstName}&
  * entreprise={!contact.Account.Name}&
  * fonction={!contact.Title}&
  * email={!contact.Email}&
  * telephone={!contact.Phone}&
  * cuser={!$User.Id}"
  */
 
    include('phpqrcode/qrlib.php');

    $tempDir = "./";

    // Nos données
    $name         = @$_GET['prenom']." ".@$_GET['nom'];
    $sortName     = @$_GET['nom'].";".@$_GET['prenom'];
    $phone        = @$_GET['telephone'];
    $phonePrivate = '';
    $phoneCell    = '';
    $orgName      = @$_GET['entreprise'];
    $email        = @$_GET['email'];
 
    // Données supplémentaires que vous pourriez exploiter
    $addressLabel     = '';
    $addressPobox     = '';
    $addressExt       = '';
    $addressStreet    = '';
    $addressTown      = '';
    $addressRegion    = '';
    $addressPostCode  = '';
    $addressCountry   = '';
 
    // we building detailled raw data
    $codeContents  = 'BEGIN:VCARD'."\n";
    $codeContents .= 'VERSION:2.1'."\n";
    $codeContents .= 'N:'.$sortName."\n";
    $codeContents .= 'FN:'.$name."\n";
    $codeContents .= 'ORG:'.$orgName."\n";
    $codeContents .= 'TEL;WORK;VOICE:'.$phone."\n";
    $codeContents .= 'TEL;HOME;VOICE:'.$phonePrivate."\n";
    $codeContents .= 'TEL;TYPE=cell:'.$phoneCell."\n";
    $codeContents .= 'ADR;TYPE=work;'.
        'LABEL="'.$addressLabel.'":'
        .$addressPobox.';'
        .$addressExt.';'
        .$addressStreet.';'
        .$addressTown.';'
        .$addressPostCode.';'
        .$addressCountry
    ."\n";
    $codeContents .= 'EMAIL:'.$email."\n";
    $codeContents .= 'END:VCARD';
 
 //Une carte Plus soft contenant que le nom et le numéro de téléphone
    $codeContents2  = 'BEGIN:VCARD'."\n";
    $codeContents2 .= 'FN:'.$name."\n";
    $codeContents2 .= 'TEL;WORK;VOICE:'.$phone."\n";
    $codeContents2 .= 'END:VCARD';

    // Generation des images
    QRcode::png($codeContents, $tempDir.'1.png', QR_ECLEVEL_L, 3);
    QRcode::png($codeContents2, $tempDir.'2.png', QR_ECLEVEL_L, 3); 
 $qr1 = $tempDir.'1.png';
 $qr2 = $tempDir.'2.png';
 
 ?>

<html>
  <head>
  </head>
  <body>
   

![](https://artiom-fedorov.blogspot.com/2014/02/%3C?=$qr1?%3E) 
    

![](https://artiom-fedorov.blogspot.com/2014/02/%3C?=$qr2?%3E) 
    

</body>
</html>

  
Ce script s'appuie sur une lib **LGPL PhpQRCode** disponible ici :  
http://phpqrcode.sourceforge.net. Vous pouvez aussi télécharger le zip de mon projet contenant la lib dont je fourni le lien en bas de cet article.  
  
Comme vous pouvez le constater lorsque le script reçoit des données fournies en paramètre un processus de formatage en chaîne de caractères est effectué. Puis on transforme la fameuse chaîne de caractères représentant les données contact sous forme d'une [vcard](http://fr.wikipedia.org/wiki/Code_QR) en image QRCode. Une intégration simpliste à destination de l'iFrame est proposée un peu plus bas dans l'article. Ce petit bout de code html vous premet de "mettre en page" la fameuse section qui sera embarquée dans la fiche contact salesforce. Passons a présent a cette fameuse intégraton.  
  
Vous aurez certainement remarqué qu'il y a deux images, il s'agit simplement d'une version complète et une version minimaliste de la fiche contact.  
  
**Appel d'un script externe grace aux iFrame avec SalesForce depuis la fiche contact**  
  
Pour avoir un maximum de liberté en ce qui concerne l'intégration je vous suggère de créer une page VisualForce qui aura comme simple but d'accueillir l'appel à notre iFrame. Je précise que d'autres techniques d'intégrations d'iFrames existent sous salesforce (je ne les développerais pas ici).  
**Pour créer une nouvelle page Visualforce suivez simplement les screenshots ci dessous**  
  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEOTimVfxoRmIV-Lfu49Fj3fPnmtyOi9Rk-wHbxKOvBxBkDJREbAUPFh0Prni5Q282jgZM9wUImcwKrb6Cuj04CpELHxFXE1hAHZ286orr64m_JwsSQSbkOd3NSqpPV1FhVqTY40M1bXU/s1600/configuration-sales-force.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEOTimVfxoRmIV-Lfu49Fj3fPnmtyOi9Rk-wHbxKOvBxBkDJREbAUPFh0Prni5Q282jgZM9wUImcwKrb6Cuj04CpELHxFXE1hAHZ286orr64m_JwsSQSbkOd3NSqpPV1FhVqTY40M1bXU/s1600/configuration-sales-force.png)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjFzGlTCjDhTZq2v1o0a_2RNPt4oyxhPN7vvXqnxUZgz3IzUihj7CenKdw-_iIqhF-cfCiIOnPZkQobB1LrLsVZzS1tX0VPl8Aj98_tgP8IgwTi1OnLRtouX2cTZDv8ZiM_E-Xf5uWEE1g/s1600/contenu-de-lintegration-iframe-salesforce.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjFzGlTCjDhTZq2v1o0a_2RNPt4oyxhPN7vvXqnxUZgz3IzUihj7CenKdw-_iIqhF-cfCiIOnPZkQobB1LrLsVZzS1tX0VPl8Aj98_tgP8IgwTi1OnLRtouX2cTZDv8ZiM_E-Xf5uWEE1g/s1600/contenu-de-lintegration-iframe-salesforce.png)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi7tw7NvXQuxaj55qOz52zUY6-3RUuY3ewOfS3OtU7LktOgaC2ZvyZIu5xai5HijU3J_laxF8XJY2n6yEogq6R_5WJicwKFQtvNVErPtdTDi32fSQodWsXggmsoF2J-FaKK8RX8dZKOPpM/s1600/cr%25C3%25A9ation-nouvelle-page-sales-force.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi7tw7NvXQuxaj55qOz52zUY6-3RUuY3ewOfS3OtU7LktOgaC2ZvyZIu5xai5HijU3J_laxF8XJY2n6yEogq6R_5WJicwKFQtvNVErPtdTDi32fSQodWsXggmsoF2J-FaKK8RX8dZKOPpM/s1600/cr%25C3%25A9ation-nouvelle-page-sales-force.png)[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqyg61vGDIRnr3bnrHhR5VuHEIrM6kElKt6EMxtvQFMRK7IrU_eFTmkE7qSdci6mBViovpYYy4SjGeRQu0WMvcvPZnbkvDcjKGBYUJut0ZboqQKk7g5rD8ByWQvGbugQuofzQsOT3FAMo/s1600/nouvelle-page-visualforce.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqyg61vGDIRnr3bnrHhR5VuHEIrM6kElKt6EMxtvQFMRK7IrU_eFTmkE7qSdci6mBViovpYYy4SjGeRQu0WMvcvPZnbkvDcjKGBYUJut0ZboqQKk7g5rD8ByWQvGbugQuofzQsOT3FAMo/s1600/nouvelle-page-visualforce.png)  

  
  
  
**Appel d'un script externe grace aux iFrame avec SalesForce**  
  
Dans la page visualforce nouvellement crée dans votre instance SalesForce nous allons mettre le code html qui réalise l'appel a l'iFrame.  

  

  
Quelques infos utiles a propos du code de templating apex:  

- L'accès aux données de la fiche courant est rendue possible en précisant dans standartController que nous allons travailler l'entité contact.
- L'accès a chaque champ rappelle un peu le moteur de templates smarty ou mustache (moteur de templates). Chaque champ est accèdé en employant la syntaxe {!controller.field}  (controlleur et nom du champ) ce qui pour le nom du contact donne:   {!contact.name}
- L'accès aux jointures du contact peut être réalisé en mettant deux noms de controlleurs à la suite. Par exemple pour accèder au nom de l'entreprise du contact nous écrirons:  {!contact.Account.name}
- Vous pouvez rendre votre appel a l'iFrame plus élégant en rendant possible le paramètrage de l'url du serveur. Dans SalesForce vous pouvez créer un paramètre personnalisé qui sera accédé 

  
**Ajout de notre visualpage au dans le template contact SalesForce.**  
  

[![Screenshot explicatif a propos de l'intégration des pages dans le template](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhpLcp01wbiX1gvj9PLa2CvKUm5suMu-7udqaP3vSzhBcTlZFEkRyl6ybDF82Q1JvEPw5Dxn7Kj7mfLvdh3cGyaUknBaLCGiDdMQTMNdu7MSC7qjnYeWdL02UFPcvRcecFGWXDxbmIyhxQ/s1600/Capture+du+2014-02-11+19:52:24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhpLcp01wbiX1gvj9PLa2CvKUm5suMu-7udqaP3vSzhBcTlZFEkRyl6ybDF82Q1JvEPw5Dxn7Kj7mfLvdh3cGyaUknBaLCGiDdMQTMNdu7MSC7qjnYeWdL02UFPcvRcecFGWXDxbmIyhxQ/s1600/Capture+du+2014-02-11+19:52:24.png)

 A présent que notre page visualforce est prête, nous allons pouvoir l'intégrer dans les fiches contacts du CRM SalesForce.  
  
Pour cela rendez vous dans la configuration de SalesForce, puis dans la section Configuration de l'application dépliez le menu Personnaliser puis Contacts puis Présentation de page. A ce moment là salesforce vous demande quel layout vous souhaitez éditer. Prenez celui qui est désigné par défaut "contact layout" Je vous invite à regarder la [documentation en ce qui concerne les layouts](http://help.salesforce.com/HTViewHelpDoc?id=customize_layout.htm&language=en_US) mais en gros l'utilité première des layouts est de pouvoir altérer la présentation des vues en fonction des utilisateurs.  
  
Une fois cela réalisé vous arriverez sur l'écran présenté dans le screenshot. Ici les choses sont très intuitives (en comparaison à certains autres CRM). Pour recevoir la page apex dans la fiche contact nous allons en premier lieu créer une section. Pour ce faire dans le menu du haut cliquez sur "champs" puis réalisez un drag and drop (glissé-déposé) à l'endroit du template où vous aimeriez placer la section. Une fois votre section disposée, vous allez toujours dans le menu du haut cliquer sur Pages Visualforce (partie de gauche du menu), puis réaliser une fois de plus un drag and drop depuis le menu du haut de la Page Visual force disponible vers la section. Une fois cette étape achevée cliquez sur Enregistrer. Vous serez en mesure de modifier la taille de votre section ainsi que le nom de celle ci en survolant les éléments nouvellement crées (regardez à gauche de ces éléments, des menus de suppression/édition apparaissent).  
  
  
**Résultat de l'intégration des QRCodes dans les fiches contact de SalesForce**  
  
Rendez-vous sur une fiche contact, rafraîchissez la page si besoin et admirez vos sublimes QRCodes.  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs5AAuF0VtMDpjiMkiflv4apQPeHibmPKctdSMVCdHjGEVRZDdNVj-v1Y9zdFZ67PCALZ8ypMMj3VOjji02qlwJxIDMa0YDuSimUKn9EFT-Y4Sv-AGVzrAyt-VA9ByUnP5tDJ1G4jvuR4/s1600/exemple+d%2527int%25C3%25A9gration+des+qrcodes+dans+salesforce.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs5AAuF0VtMDpjiMkiflv4apQPeHibmPKctdSMVCdHjGEVRZDdNVj-v1Y9zdFZ67PCALZ8ypMMj3VOjji02qlwJxIDMa0YDuSimUKn9EFT-Y4Sv-AGVzrAyt-VA9ByUnP5tDJ1G4jvuR4/s1600/exemple+d%2527int%25C3%25A9gration+des+qrcodes+dans+salesforce.png)

  
  
**Remarques importantes a propos de ce petit projet.**  
  
Mon article est un exemple d'intégration didactique. N'utilisez pas ce script dans un environnement de production de grande envergure. En effet les images ici sont régénérées à chaque affichage ce qui à le mérite de mettre à jour le qrcode du contact instantanément suite à une modification du dit contact mais qui est très **couteux niveau calcul côté serveur**. Cela étant dit, si vous déposez votre script sur un serveur mutualisé comme OVH par exemple, vous pourrez utiliser ce script dans des organisations de petite taille.  
  
Une optimisation très simple à faire sur ce script pour le rendre utilisable à grande echelle serait de faire un hash de la chaîne de carracteres représentant la vcard en md5 et de nommer le fichier image contenant le qrcode par le md5 obtenu. Ensuite au lieu de generer le QRCode à chaque fois, on testera l'existance du fichier dont le nom correspond au md5 de la vcard. Si ce dernier n'existe pas on le génère sinon on va chercher le fichier existant. L'altération de la fiche contact générera une chaine VCARD différente et donc un md5 différent, donc le fichier image sera alors généré à nouveau. Le temps réel est préservé, par contre si les utilisateurs altèrent très souvent les fiches contacts attention à l'espace que peux finir par occuper le cache du script.