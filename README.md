### Description de student-list

Ce répertoire est une application simple pour lister les étudiants avec un serveur web (PHP) et une API (flask)

### Contexte du projet : 
POZOS est une société informatique située en France qui développe des logiciels pour les écoles secondaires.
Le département d'innovation veut bouleverser l'infrastructure existante pour qu'elle puisse être évolutive, facilement déployée avec un maximum d'automatisation.
POZOS veut que vous construisiez un POC pour montrer comment docker peut vous aider et combien cette technologie est efficace.
Pour ce POC, POZOS va vous donner une application et vous demander de construire une infrastructure "découplée" basée sur Docker.

### Existant du projet :
Actuellement, l'application tourne sur un seul serveur, sans aucune extensibilité ni haute disponibilité.
Lorsque POZOS a besoin de déployer une nouvelle version, à chaque fois quelque chose ne va pas.
En conclusion, POZOS a besoin d'agilité sur sa ferme logicielle.

### Quelques récommandations pour infrastructure :
Pour ce POC, vous n'utiliserez qu'une seule machine avec un docker installé dessus.
La construction et le déploiement seront effectués sur cette machine.
POZOS vous recommande d'utiliser l'OS Centos7.6 car c'est le plus utilisé dans l'entreprise.
Veuillez également noter que vous êtes autorisé à utiliser une machine virtuelle basée sur Centos7.6 et non votre machine physique.
La sécurité est un aspect très critique de POZOS DSI donc s'il vous plaît ne désactivez pas le pare-feu ou d'autres mécanismes de sécurité sinon veuillez expliquer vos raisons dans votre livraison.

### Description de l'application :
L'application sur laquelle vous allez travailler s'appelle "student list", cette application est très basique et permet à POZOS d'afficher la liste des étudiants avec leur âge.

## Student list a deux modules :
le premier module est une API REST (avec authentification de base nécessaire) qui envoie la liste des souhaits de l'étudiant basé sur un fichier JSON.
Le second module est une application web écrite en HTML + PHP qui permet à l'utilisateur final d'obtenir la liste des étudiants.

Votre travail consiste à construire un conteneur pour chaque module et à les faire interagir les uns avec les autres.
Les fichiers que vous devez fournir (dans votre livraison) sont Dockerfile et docker-compose.yml (actuellement les deux sont vides)

Il est maintenant temps de vous expliquer le rôle de chaque fichier ;
- Docker compose.yml : pour lancer l'application (API et application web)
- Dockerfile : le fichier qui sera utilisé pour construire l'image de l'API (les détails seront donnés)
- Student age.Json : contient le nom de l'étudiant avec son âge au format JSON
- Student age.py : contient le code source de l'API en python
- Index.php : Page PHP où l'utilisateur final sera connecté pour interagir avec le service pour lister les étudiants avec leur âge.

Vous devez mettre à jour la ligne suivante avant de lancer le conteneur du site web pour que le nom d'api ip ou nom et le port correspondent à votre déploiement $URL = http://<nom d'api ip ou nom: port>/pozos/api/v/get_student_ages' ;

## Build et test :
Quelles informations pour la construction du conteneur :
  => image de base : "python: 2.7-stretch"
  => Mainteneur :  nom_ops
  => Ajouter le code source : Vous devez copier le code source de l'API dans le conteneur à la racine du chemin "/"
 
  # Prérequis
L'API utilise le moteur FLASK, voici une liste des paquets que vous devez installer :

       apt-get update -y && apt-get install python-dev python3-dev libsasl2-dev python-dev libldap2- dev libssl-dev -y
       pip install flask==1.1.2 flask_httpauth==4.1.0 flask_simpleldap python-dotenv==0.14.0
 => Volume : creer un dossier data à la racine root "/" ou les données seront stockées et la declarées
 => API Port : expose port 5000
 => CMD : CMD [ "python", "./student_age.py" ]
 
Construisez votre image et essayez de l'exécuter (n'oubliez pas de monter le fichier student_age.json dans /data/student_age.json dans le conteneur), vérifiez les journaux et assurez-vous que le conteneur écoute et est prêt à répondre.

     curl -u toto:python -X GET http://<host IP>:<API exposed port>/pozos/api/v1.0/get_student_ages
     
## Infrastructure as Code :
Après le test de ton API image, vous avez besoin de tout mettre ensemble et déployer cela en utilisant le docker-compose.yml

 
 
