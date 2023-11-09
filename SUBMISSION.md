
  # Évaluation docker

MZEBLA Faouizi & GOMES VITORINO Marvin

## Sommaire

 - [Introduction](#introduction)
 - [Connexion à la machine virtuelle](#connexion-à-la-machine-virtuelle)
 - [Gestion des images](#gestion-des-images)
 - [Mise en place des containers](#mise-en-place-des-container)
 - [Résultat](#resultat)
 - [Conclusion](#conclusion)

## Introduction

Nous allons mettre en place une application de vote avec l'affichage des résultats en direct.
Cette application contient plusieurs micro services qui seront hébergés sur notre machine virtuelle et accessible depuis notre machine locale.
Chaque service utilisera un container Docker. Tous ces containers tourneront sur notre VM.

## Connexion à la machine virtuelle
Nous allons nous connecter à la machine virtuelle via la fonction SSH. Nous utiliserons la même machine virtuelle que pour l'évaluation précédente.

![](https://cdn.discordapp.com/attachments/751435338911711284/1167448442986041448/image.png)

Nous utilisons la commande scp pour copier nos fichier locaux vers la machine virtuelle.

![](https://cdn.discordapp.com/attachments/751435338911711284/1172132341402058783/image.png)


## Gestion des images
  ### Création du fichier de build des images
   Nous allons crée un fichier docker-compose.build.yml pour créer toute nos images a partir des Dockerfile fournit dans l'énoncé.
   Voici le fichier : 
   ![](https://cdn.discordapp.com/attachments/751435338911711284/1172133161396871228/image.png)

Une fois le fichier créer et envoyé sur la machine virtuelle nous executons cette commande (sur la machine virtuelle) : 

![](https://cdn.discordapp.com/attachments/751435338911711284/1172133688398581840/image.png)

   ### Création des tags des images
   
   Nous exectons la commande pour tag toutes nos images que nous venons de créer
   ![](https://cdn.discordapp.com/attachments/751435338911711284/1172136973465567272/image.png)
   
### Mise en ligne des images
Nous allons ensuite push toutes nos images sur notre repository public et privé.

![](https://cdn.discordapp.com/attachments/751435338911711284/1172137397622935592/image.png)

## Mise en place des container
### Création du compose.yml
Nous allons créer le fichier compose.yml qui va nous permeterre via la commande :

    docker compose up -d
   
   de lancer plusieurs containers en même temps.
   Nous allons aussi créer le volume et les networks dans le fichier docker compose.
   
![](https://cdn.discordapp.com/attachments/751435338911711284/1172168838612271194/Capture20dE28099eCC81cran202023-11-0920aCC802014.png)
    
Nous avons utiliser les réseaux :
 **front** & **back** pour lier les services front entre eux et les services back entre eux.

Il y a aussi un volume db-data pour la DB Postgres.

## Résultat

Voici les containers qui tournent sur notre machine virtuelle : ![](https://cdn.discordapp.com/attachments/751435338911711284/1172168144601751592/image.png)

### Port forwarding
Nous allons faire du port forwarding pour pouvoir avoir accès aux ports 5000 & 5001 depuis notre machine **locale**. Nous faisons ces configurations sur VitualBox dans les paramètres de notre VM.

![](https://cdn.discordapp.com/attachments/751435338911711284/1172170787822776340/image.png)

### Résultat sur internet

![](https://cdn.discordapp.com/attachments/751435338911711284/1172167907485159514/image.png)

Nous avons bien nos deux applications qui tournent et qui sont disponible sur notre machine locale via le port 5000 et 5001

## Conclusion

Nous avons mis en place deux applications nécessitant plusieurs micro services. Ces services sont reliés entre eux. Nous les avons exposés sur notre machine locale et nous pouvons avoir accès à ces applications via l'url : localhost:5000 ou localhost:5001 pour les résultats.

Nous avons utilisé docker compose afin de pouvoir créer rapidement plusieurs containers en même temps.
Deplus ces micro services tournent sur la machine virtuelle et sont accessibles depuis la machine locale.
