# Etape 1

## 1. Qu'est-ce qu'une machine virtuelle ?

Une machine virtuelle est un environnement logiciel qui reproduit une machine informatique (plusieurs possibles par machine).
Elle offre un OS (qui fonctionne comme s'il disposait de sa propre machine), des ressources matérielles virtuelles, peut éxecuter son propre système d'exploitation et ses applications en partionnant les ressources de la machine de physique (hôte).

## 2. Deux avantages de la virtualisation en entreprise

La virtualisation permet :
- de lancer plusieurs machines sur un seul serveur (cout materiel réduit)
- permet aussi de tester des logiciels sans risques (isolation)
- environnement propre


## 3. Difference avec le travail direct sur l'ordinateur

Quand on travaille directement sur son ordinateur, on modifie le systeme principal.
Si on fait une erreur, cela peut avoir un impact sur toute la machine.
- Reproductibilité 
- Isolation

## Étape 2

## 1. Qu'est-ce qu'un conteneur Docker ?

Un conteneur Docker est un environnement adapté pour le lancement d'une application. Il contient l'application ainsi que des librairies, une configuration et des fichiers utiles (en gros ce qui est nécessaire au fonctionnement à l'application (runtime)).

## 2. Difference entre une machine virtuelle et un conteneur

Une machine virtuelle emule une machine complèté (OS et ressources comprises)
Un conteneur est plus leger et partage le systeme de la machine hôte. L'isolation s'arrête à l'application et son environnement.

## 3. Pourquoi les conteneurs sont utiles dans le Cloud ?

Les conteneurs sont faciles et rapides à deplacer d'une machine à une autre.
Ils demarrent vite et utilisent moins de ressources qu'une machine virtuelle. Les contenairs peuvent être agglomérer en noyau.
Ils permettent de lancer plusieurs copies de la meme application rapidement.

## Etape 3

## 1. Pourquoi un Dockerfile est preferable a la configuration manuelle d'un conteneur ?

Un Dockerfile permet de decrire toute la configuration dans un fichier. On peut reconstruire la meme image, l'instancier plusieurs fois ou la modifier plus aisément grâce au Dockerfile. Fonctionne de paire avec l'automatisation (qui arrivera plus tard).

## 2. Difference entre une image Docker et un conteneur Docker

Une image Docker contient l'application, les dependances et la configuratio alors que le conteneur Docker est une image instanciée, en cours d'exécution.
