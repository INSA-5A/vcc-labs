# Etape 1

## 1. Quel est le rôle de VM-K8s dans l’architecture mise en place ? Quelle est la différence entre cette machine et les nœuds workers ?

VM-K8s est l'orchestrateur, il organise et gère les tâches à effectuer tandis que les workers sont les exécutants. Ils s'occupent de réaliser les tâches que le master leurs attribue.

## 2. Pourquoi le Docker Registry et le master Kubernetes sont-ils installés sur deux VMs différentes ?

Le Registry conserve et distribue les images Docker. VM-K8s s'occume de gérer ces images. Les séparer permet de libérer les ressources de chaque VM pour qu'elle puisse se concentrer sur ses propres tâches.
Cela permet aussi de les rendre indépendants, si la VM de l'un ne fonctionne plus, elle n'impacte pas l'autre.

## 3. Le script d’installation vous a permis d’installer Kubernetes sans exécuter manuellement toutes les commandes nécessaires. Citez les opérations importantes réalisées par le script master et expliquez très brièvement en quoi elles sont nécessaires au fonctionnement du cluster.


1 - Désactivation du swap :
le système de swap rends la mémoire non prévisible et peux dégrader considérablement le service d'un worker sans provoquer de changements.

2 - Configuration du noyau et du network :
Activation du transfert IP nécessaire au fonctionnement du réseau des conteneurs.

3 - Installation de containerd :
Exécute les conteneurs, avec une gestion des ressources 

4 - Installation de kubelet, kubeadm et kubectl :
 Gérer les Pods, initialiser le cluster et l’administrer. 

5 - Initialisation avec kubeadm init :
Configure le plan de contrôle, l’adresse de l’API et la plage d’adresses des Pods.

6 - Configuration de kubectl :
Donne les accès administrateur, pour pouvoir gérer le cluster.

7 - Génération de la commande de rattachement :
Permet aux workers de rejoindre le cluster.

---

# Etape 2

## 1. Quel est le rôle d’un Deployment dans Kubernetes ? Pourquoi ne déploie-t-on pas directement un Pod ?

Un Deployment maintient le nombre de Pods souhaité et permet des mises à jour progressives.
L'intérêt de passer par un deployment est qu'il assure le remplacement du pod en cas de panne par exemple.

## 2. Quelle est la différence entre une image Docker, un Pod et un Deployment ? Comment les 3 sont-ils liés ?

L’image Docker contient l’application et ses dépendances pour l’exécuter de façon reproductible.
Le Pod héberge les conteneurs issus de cette image.
Le Deployment gère les Pods pour faciliter leur réplication, leur remplacement et leurs mises à jour.

## 3. Expliquez le principe de réconciliation. Quelle composante Kubernetes est responsable de ce comportement ?

La réconciliation veille sur la différence entre l’état réel à l’état souhaité et corrige les écarts, par exemple en recréant un Pod manquant.
Ce sont les contrôleurs du kube-controller-manager, notamment Deployment et ReplicaSet, qui automatisent le maintien de l’application.

---

# Etape 3

## 1. Pourquoi ne peut-on pas simplement utiliser l’adresse IP du Pod calculator-calc pour permettre à un utilisateur d’accéder à l’application ?

L'ip d'un pod change lorsqu'il est recrée.

## 2. Comment Kubernetes sait-il que le Service calculator-calc doit transmettre les requêtes au Pod de calculator-calc ?

Au donne des labels au pods qui orrespondent au app:name ainsi le registre/DNS de Kubernetes peut orienter les paquets vers le pod associé.

## 3. Quelle est la différence entre le port exposé, le port cible et le NodePort utilisés dans votre architecture ?

Port exposé : Le port de contact (acessible depuis "l'exterieur")
Port cible : Port sur lequel l'application ecoute dans le pod (ici 5000X) 
NodePORT : Permet d'accéder aux services depuis l'exterieur (port utilise pour le curl du sujet) en exposant un service sur un port de la VM qui heberge le noeud.

---

# Etape 4

## 1. Pourquoi les quatre microservices utilisent-ils un port de type ClusterIP, tandis que calc-service utilise un port de type NodePort ?

ClusterIP est un type de ressource Kubernetes qui permet à un service de se voir attribuer une IP valide uniquement dans le cluster. Ca protege les services de l'exterieur pour qu'ils ne soient joignables que par l'application. Un utilisateur lui n'a acces depuis l'exterieur qu'à l'application et pas aux services.

## 2. comment Kubernetes permet-il au frontend de contacter le backend sans connaître l’adresse IP du Pod ?

Il utilise le DNS de son service (http://sum-service:50001). L'ip n'est donc plus nécessaire.

## 3. On propose de configurer le frontend avec l’adresse IP actuelle des Pods backend (sum, sub...), par exemple "http ://10.x.x.x :<PORT>". Pourquoi cette solution n’est-elle pas adaptée à Kubernetes ?

L'ip d'un pod peut changer après suppression, et un pod n'est pas une ressource permanente. Après suppression le nouveau pod ne sera plus joignable par IP alors qu'en revanche le nom ne change pas.

