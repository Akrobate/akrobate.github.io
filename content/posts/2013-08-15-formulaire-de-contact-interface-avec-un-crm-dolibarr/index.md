---
date: '2013-08-15T14:05:20+02:00'
draft: false
title: Formulaire de contact interfacé avec un CRM Dolibarr
slug: formulaire-contact-crm-dolibarr
tags:
  - CRM
  - informatique
  - php
categories:
  - Web
cover:
  image: 1-formulaire-site-rempli.avif
  alt: "Exemple de formulaire integré avec le CRM dolibarr"
description: Découvrez comment synchroniser automatiquement les formulaires de contact de votre site web avec votre CRM Dolibarr grâce à une solution simple en PHP/JS. Centralisez vos prospects et gagnez en efficacité !
showTOC: true
---

![](1-formulaire-site-rempli.avif)
{ .article-image-left mode="lightbox" miniature-width=200 }

![](4-fiche-evenement-cree.avif)
{ .article-image-right mode="lightbox" miniature-width=200 }

Lorsque l'on **crée un site** internet pour des besoins professionnels on est souvent amené à **mettre en place un formulaire de contact**, de demande de devis, ou toute autre demande. La question qui se pose souvent est comment **tirer un maximum d'avantages de ces précieuses pistes** de prospects qui s'ouvrent à vous. La réponse apportée par la plus part des structures simples est le renvoi automatique du formulaire de contact ou autre sur une boite mail. Une personne sera alors chargée de traiter ces demandes manuellement une à une. La solution que je vous propose est l'intégration directe de vos formulaires de prise de contacts dans votre CRM Dolibarr. **Les prises de contacts seront automatiquement ajoutées dans Dolibarr en tant que tâches** dans l'agenda, de fait le traitement de ces dernières s’intègrent en toute fluidité à un process d'entreprise s'appuyant sur un CRM.


## Pourquoi utiliser un CRM même dans une structure de petite taille?
  
Je ne m'attarderais pas ici sur l'intérêt pour une entreprise de taille moyenne voir une grande multinationnale d'utiliser un outils de gestion de la relation client (CRM). En effet la réponse parait évidente grande quantité de client et beaucoup d'échanges amènent un besoin immédiat d'organisation et de centralisation des données. Beaucoup de grands groupes optent pour des solutions de cloud CRM (tels que Salesforce par exemple) onéreuses au premier abord, mais disponibles et opérationnelles immédiatement sans aucun besoin en infrastructure ni en maintenance.  
Je pense qu'en ce qui concerne les petites entreprises, voir les autoentrepreneurs l'utilisation d'un CRM libre tel que Dolibarr ou Sugar peut s’avérer être d'une redoutable efficacité. En effet avoir un suivi détaillé de chaque client, des diverses prestations effectués et des tarifs pratiqués permet d'avoir une aide décisionnelle non négligeable pour le développement de son activité. Souvent dans les petites structures les gérants n'ont pas réellement d'outils de monitoring pour voir l'évolution de l'activité en temps réel afin d'optimiser sa prise de décision. Un CRM tel que dolibarr fournit par défaut quelques outils et indicateurs vitaux dans la gestion d'une structure. Je vous invite a découvrir les différentes fonctionnalités en détail de [dolibarr](http://www.dolibarr.fr/) par exemple qui me parait être une solution plus que correcte pour une entreprise de petite taille.  

{{% gallery %}}

![](1-formulaire-site-rempli.avif)
{ mode="lightbox" miniature-width=200 }

![](2-dolibarr-tableau-de-bord.avif)
{ mode="lightbox" miniature-width=200 }

![](3-evenement-cree.avif)
{ mode="lightbox" miniature-width=200 }

![](4-fiche-evenement-cree.avif)
{ mode="lightbox" miniature-width=200 }

![](5-gmail-evenement-recu.avif)
{ mode="lightbox" miniature-width=200 }

{{% /gallery %}}


## Pourquoi centraliser ses prises de contact dans un CRM tel que Dolibarr
  
**Dolibarr** comme beaucoup d'autres outils **possede une gestion de tâches et de rappels de tâches**. Une réponse a une prise de contact est une tâche par excellence. Souvent fortement sous utilisés les rappels de tâches est un outils d'une grande efficacité. Imaginez maintenant que **a chaque fois que quelqu'un prend contact** avec vous sur l'un de vos sites internet **cela** **crée automatiquement une tâche dans votre CRM** avec de fait toutes les **régles métier CRM s'appliquant dessus**. Par exemple sous Dolibarr une tâche crée incrémentera automatiquement le nombre de tâches a faire ou en retard au niveau du tableau de bord de la page d'accueil. En cliquant sur la tâche fraichement crée l'utilisateur pourra consulter les réponses a l'ensemble des champs saisis sur la page d'accueil.  
**Une solution simple et rapide**  
  
Je vous propose une solution un peu "**Quick and Dirty**" mais qui à le mérite de fonctionner parfaitement et de n'exiger que quelques minutes de mise en place pour un fonctionnement robuste. La mécanique se limite à l'utilisation de trois scripts. Il s'agit de:  
  
- **crm.script.js** - hébergé sur le site frontal. Chargé de sérialiser l'ensemble des donnés d'un formulaire ciblé, effectue une première vérification de la non nullité des champs.  
- **crm.sender.php** - hébergé sur le site frontal. Chargé de créer une clef pour la vérification des donnés et pour l'autorisation de soumettre au script hôte. Peut aussi au besoin effectuer des vérifications de formulaire.  
- **doliscript.php** - hébergé sur le même hébergement que votre instance de dolibarr. Chargé de vérifier les donnés envoyés par le script crm.sender.php, les ajoute directement la prise de contact en tant qu’événement dans la base de donnés Dolibarr.  
  
  
## Schéma du principe de fonctionnement

![](Script-working-process-connector-dolibarr-contact.avif)
{ mode="lightbox" }
  
## Principe de fonctionnement détaillé et code source de la solution.
  
 Pour bien comprendre comment tout cela fonctionne partons du début. Le fichier html contentant le code html du formulaire de contact devra contenir l'inclusion du fichier crm.script.js. Ajoutez l'id "contactCRM" à La déclaration de formulaire. A présent tous les champs contenus dans le formulaires seront sérialisés et transmis en ajax au script crm.sender.php. Le fichier js permet de faire des tests simplistes de non nullité des champs en ajoutant la classe crmdata au champ qui devra être sensibilisé a la non nullité.  

Exemple de fichier html contenant le balisage nécessaire:  

Pour une demande de devis
  
### Le fichier `crm.script.js`

```javascript
$(document).ready(function() {
  $('#contactCRM').submit( function(e) {
    e.preventDefault();
    var ok = true;
    $(this).find('.crmdata').each(function() {
      if ($(this).val() == "") {
        ok = false;
        $(this).addClass('error');
      } else {
        $(this).removeClass('error');
      }
    });

    var datasave = $(this).html();

    if (ok) {
      var datas = $(this).serialize();
      $(this).fadeOut('slow', function() {
        $(this).empty();
        $(this).append('<img src="images/ajax-loader.gif" />');
        $(this).fadeIn('slow', function() {
          $.ajax({
            type: 'POST',      
            url: "crm.sender.php",
            data: datas,     
            success: function(msg) {
              $('#contactCRM').find(".alert-box").fadeOut("slow", function() {
                $('#contactCRM').find(".success").fadeIn('slow');
              });
            },
          });
        });
      });
    }
  });
});
```


Comment vous pouvez le voir le contenu du formulaire est envoyé au script se situant a la meme adresse que la page contact et ayant pour nom crm.sender.php. Nous allons justement voir plus en détail ce fichier.  
  
### Le fichier `crm.sender.php`

```php
// Config
$passphrase = "votrepassphrase";
$url_dolibarr = "http://adresseversvotredoliscript.com";

$global_data = array_merge($_POST, $_SERVER);
/* Exemple d'intégration de regles de controle simples. Le fichier 
crm.script.js devra apporter les traitements adéquat dans sa
condition de retrour data de l'appel ajax (commenté)

$error = false;
$errorType = "";

if ($post['nom'] == "") {$error = true; $errorType = 'nomunset';}
if ($post['prenom'] == "") {$error = true; $errorType = 'prenomunset'; }
if ($post['mail'] == "") { $error = true; $errorType = 'mailunset';}
if ($post['message'] == "") {$error = true; $errorType = 'messageunset';} */

$jsonstr = json_encode($global_data);
$key = md5($passphrase . date('d') . $jsonstr);
$url = $url_dolibarr . "/doliscript.php?key=$key&data=".urlencode($jsonstr);

//exec requette
$response = file_get_contents($url);

echo($response);
```
  
Le fichier crm.sender.php prépare une clef $key qui est composée de la passphrase qui doit etre commune aux deux scripts crm.sender.php et doliscript.php. Cette passphrase est une sorte de mot de passe permettant d'authentifier la demande d'ajout de datas. Par ailleurs comme vous pouvez le constater dans le script la chaîne représentant les datas sérialisées fait partie du hash pour obtenir la clés. De fait cette clef a un double usage. Vérifier que l'utilisateur qui envoi les données a bien le droit de les envoyer ainsi que de vérifier l'intégrité des données lors de la transmission entre les deux scripts.  
  
### Le fichier `doliscript.php`
  
Ce fichier doit impérativement être placé a la racine de votre instance dolibarr. Donc potentiellement sur un serveur différent de votre frontal. Le script crm.sender.php comporte la ligne de conf $url_dolibarr = "http://ladressedevotredolibarr", c'est ici que vous aurez a indiquer le chemin vers le script doliscript.php distant.  


```php
//config
$passphrase = "votrepassphrase";
include_once("conf/conf.php");

$user_author = 3; // id de l'utilisateur créant la tache
$user_done = 2;  // id de l'utilisateur a qui la tache est assigné
$user_action = 2; // id de l'action

$data = $_GET['data'];
$key = $_GET['key'];
$data = stripslashes($data);
 
$genkey = md5($passphrase . date('d') . $data);
  
if ($genkey != $key) {
  echo('error');
  exit();
}
 
$arrdata = json_decode($data, true);

 //***** MAIL SENDING *******/
 $to = "monmail1@quelquechose.com,monmail2@quelquechose.com";
 $subject = "Prise de contact de " . $arrdata['prenom'] . " " . $arrdata['nom'];
 mail($to, $subject, print_r($arrdata, true));
 
 //**** DOLIBARR ADDING ******/
 $label = "Contact avec " . $arrdata['prenom'] . " " . $arrdata['nom'];
 $text = "
Nom: 	".$arrdata['nom']."
Prenom: 	".$arrdata['prenom']."
E-Mail: 	".$arrdata['email']."
Message: 	".$arrdata['message']."
";
 
 // Create connection
$con= new mysqli($dolibarr_main_db_host, $dolibarr_main_db_user, $dolibarr_main_db_pass,$dolibarr_main_db_name);

 // Check connection
 if ($con->connect_errno) {
  echo "Failed to connect to MySQL: " . $con->connect_error();
 } else { 
  echo "Connection was OK!\n";
 }
  
 $text = $con->real_escape_string(stripslashes($text));
 $label = $con->real_escape_string(stripslashes($label));
 
 $query="
  INSERT INTO `lyndayogdolibarr`.`llx_actioncomm` (
    `entity`,
    `datep`,
    `fk_action`,
    `label`,
    `datec`,
    `tms`,
    `fk_user_author`,
    `fk_parent`,
    `fk_user_action`,
    `fk_user_done`,
    `fulldayevent`,
    `punctual`,
    `percent`,
    `note`
  )

  VALUES (
    '1',
    NOW(), 
    '4',
    '".$label."',
    CURRENT_TIMESTAMP,
    CURRENT_TIMESTAMP,
    '".$user_author."',
    '0',
    '".$user_action."',
    '".$user_done."',
    '0',
    '1',
    '0',
    '".$text."'
  );";

  if (!$con->query($query)) {
    printf("Error: %s\n", $con->error);
  }
 
echo("Remote Ok!");
```
  
Je vous invite à regarder toutes les parties commentés consernant la configuration. Vous y trouverez directement tout ce qu'il vous faut savoir pour ajuster le fonctionnement de ces petits scripts. Le script doliscript.php s'appuie directement sur les variables de configuration de votre instance dolibarr. Chaque événement dans dolibarr possède des infos comme qui a crée l’événement, qui sera chargé d’exécuter la tache, etc. Ces informations sont entrées en dur directement dans le script doliscript au niveau des variables $user_author, etc.


## Remarques sur la solution proposée.
  
Attention cette solution simpliste comporte des défauts importants si vous souhaitez mettre cette solution en place pour un environnement en évolution. Ici je n'utilise  pas l'API de Dolibarr pour ajouter les tâches, nous **interagissons directement avec le modèle de données de dolibarr en mysql**. Cela constitue un **défaut potentiel** si le modèle de dolibarr venait à trop changer.Une manière plus élégante serait d’implémenter l'utilisation de l'api dolibarr dans le doliscript.php  
  
Cette solution à été testé sur les versions  de 3.2.X de dolibarr jusqu'à la version actuelle (3.3.2)  
  
  
## Annexe: liens vers les projets cités dans les articles

- [Lynda-Yoga.com](http://lynda-yoga.com/)  
- [Dolibarr portail france](http://www.dolibarr.fr/)  
- [Téléchargement de dolibarr](http://sourceforge.net/projects/dolibarr/files/Dolibarr%20ERP-CRM/)
