# Etape 1

## 1. Quel est le rôle d’un réseau privé dans une infrastructure Cloud ? D’un routeur externe ?

Un réseau privé permet de faire communiquer les machines virtuelles entre elles tout en les isolant du réseau public.
Le routeur externe permet de relier ce réseau privé au réseau public et de rendre certaines VM accessibles depuis l'extérieur grâce aux IP flottantes.

## 2. Pourquoi un fournisseur Cloud propose-t-il autant de catégories de ressources différentes ?

OpenStack est une plateforme IaaS (Infrastructure as a Service) qui fournit différentes ressources (VM, réseaux, routeurs, stockage, etc.) afin de permettre aux utilisateurs de construire et configurer leur propre infrastructure.
La réponse est donc pour le contrôle fin sur l'ensemble de la chaine de déploiement.

## 3. En observant la topologie générée par OpenStack, expliquez le chemin emprunté par un paquet réseau envoyé depuis l’extérieur vers une machine virtuelle sur net-discovery.

Le paquet arrive par le réseau public, passe par le routeur externe, qui utilise l'IP flottante pour le rediriger vers l'adresse IP privée de la VM sur net-discovery (via DNAT).
Sans IP flottante associée, le paquet n'atteint jamais la machine virtuelle sur net-discovery.

---

## Étape 2

## 1. Quelles sont les étapes nécessaires pour pouvoir se connecter en SSH à une nouvelle machine virtuelle OpenStack depuis la machine hôte ?

Créer une paire de clés SSH lors de la création de la VM, lui associer une IP flottante, autoriser le trafic SSH dans le groupe de sécurité, puis se connecter avec la commande ssh -i.

## 2. Quel est le rôle de l’adresse IP privée, de l’adresse IP flottante et des Groupes de Sécurité dans cette connexion ?

L'IP privée permet la communication au sein du réseau privé. L'IP flottante rend la VM accessible depuis l'extérieur. Les groupes de sécurité filtrent le trafic réseau autorisé, notamment les connexions SSH.

## 3. Pourquoi OpenStack distingue-t-il une adresse IP privée d’une IP flottante publique, plutôt que d’attribuer directement une adresse publique à chaque machine virtuelle ?

Cela permet d'économiser les adresses IP publiques celles-ci étant en quantité limitée, de renforcer l'isolation des VM et de réattribuer facilement une IP flottante à une autre machine virtuelle.

---

## Etape 3

## 1. Pourquoi les Security Groups sont-ils indispensables même lorsqu’une machine virtuelle possède une adresse IP publique ?

Les Security Groups filtrent le trafic entrant et sortant. Une IP publique ne suffit donc pas à rendre un service accessible : il faut également autoriser le port utilisé, ici le port TCP 5000.

## 2. Décrivez le chemin parcouru par une requête HTTP envoyée depuis votre ordinateur jusqu’à l’application hello-api exécutée sur votre machine virtuelle.

La requête arrive sur l'IP flottante via le réseau public, passe par le routeur OpenStack, puis est redirigée vers l'IP privée de la VM. Le groupe de sécurité autorise le trafic TCP sur le port 5000, permettant à la requête d'atteindre l'application hello-api.

---

## Étape 4

## 1. Quelles différences existe-il entre une image officielle et un snapshot ?

...

## 2. Quels avantages apporte le redimensionnement d’une machine virtuelle dans un environnement Cloud ?

...

## 3. Dans quels contextes un administrateur système préférera-t-il créer une nouvelle machine à partir d’un snapshot plutôt que de repartir d’une image vierge ?

...

