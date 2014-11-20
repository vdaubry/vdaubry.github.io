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

