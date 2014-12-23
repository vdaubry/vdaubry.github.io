---
layout:     post
title:      "Creating a web app with angularjs and parse hosted on AWS S3"
subtitle:   "How to get from idea to an online webapp in a day"
date:       2014-10-20 12:00:00
author:     "Vincent Daubry"
header-img: "img/post-bg-01.jpg"
---

Appli web + mobile : Parse.com + angular + phonegap
Where2Work

Step 1 : Une web app fonctionnel en moins d'1j

Objectif : Tester parse.com , web app fonctionnel en ligne le plus rapidement possible
Outils : Yeoman, angular, bootstrap, parse.com

Pitch Where2Work

Expliquer les étapes
Scaffolding avec Yeoman
Intégration parse + angular
Geoloc + api google maps (geocoding, reverse geocoding, embedded maps)
Déploiement site static sur S3 (route 53, cloudfront, etc) : tache aws-grunt + config aws
=> Setup 2 bucket
- root domain bucket : enable static hosting
- www bucket : Redirect all requests to another host name (rediriger vers root)
- Setup route53
- Copier les DNS dans le manager OVH (ajouter dans DNS management et pas dans DNS Zone)


Lien vers code sur github

Feedback :
Parse :
Bien pour POC, hackathon, mais cloud code pas industriel
Je l'utiliserais en prod sur des toutes petites appli : très peu de table, uniquement du CRUD, pas ou peu de logique coté serveur (validation de form, pas plus)
Je ne l'utiliserais pas en prod autre chose, si j'avais besoin de limiter la charge d'ops je partirais plutôt sur Heroku



Google maps API :
Google console :

Dans le menu "APIs" :
Ajouter Google Maps Embed API

Dans "credentials" ajouter une browser key

La clef sera visible de tout le monde. Si la sécurité n'est pas un sujet pour vous et que vous êtes ok pour que votre clef soit utilisé par d'autres personnes que vous (you fool) :

No security : laisser referers vide et valider (Any referer allowed))

Ajouter referers :
localhost:9000/*
where2workapp.com/*
*.where2workapp.com

https://developers.google.com/console/help/new/#whitelistingbyip

Pour aws ajouter : *.amazonaws.com/where2workapp.com/*

Si vos referer sont mal configuré vous aurez une erreur

"The Google Maps API server rejected your request. This IP, site or mobile application is not authorized to use this API key."


Si vous deployer sur un bucket S3, ajoutez : *.amazonaws.com

Attention votre clef sera alors utilisable par qu'elle appli servi depuis sur S3.

Attention il faut quelques minutes pour que les modifications soient prises en compte. Par exemple lorsque vous ajouter une nouvelle clef ou que vous re-générer une clef, vous verrez un message

"The Google Maps API server rejected your request. The provided API key is expired."

- - - - -
How to quickly test an idea with a webapp an no server :  angularjs + parse.com + static website en AWS S3

Expliquer concept Where2work

Step 1 :
Appli angular + geoloc Google

Step 2
Parse.com backend
Rex :
Simple
Marche bien
Bon pour un poc, ou un hackathon mais pas plus : cloud code inutilisable, pas moyen de lancer en local, le debug se fait avec des log que l'on deploie. Sans parler qu'il n'y a pas de test. Des petites validations ou des choses simples mais on ne développe rien de sérieux comme ça.


Step 3:
Deploiement S3 avec grunt-aws
Utilisation de S3 static website
Prendre un nom de domaine sur OVH
Utiliser Route 53 comme DNS


step 4 :
Ionic => faire un client iOS + Android



