# Etape 1

## 1. Quel est le rôle de VM-K8s dans l’architecture mise en place ? Quelle est la différence entre cette machine et les nœuds workers ?

VM-K8s est l'orchestrateur, il organise et gère les tâches à effectuer tandis que les workers sont les exécutants. Ils s'occupent de réaliser les tâches que le master leurs attribue.

## 2. Pourquoi le Docker Registry et le master Kubernetes sont-ils installés sur deux VMs différentes ?

Le Registry conserve et distribue les images Docker. VM-K8s s'occume de gérer ces images. Les séparer permet de libérer les ressources de chaque VM pour qu'elle puisse se concentrer sur ses propres tâches.

## 3. Le script d’installation vous a permis d’installer Kubernetes sans exécuter manuellement toutes les commandes nécessaires. Citez les opérations importantes réalisées par le script master et expliquez très brièvement en quoi elles sont nécessaires au fonctionnement du cluster.


1 - Désactivation du swap :
la configuration mémoire attendue.

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

...

## 2. Quelle est la différence entre une image Docker, un Pod et un Deployment ? Comment les 3 sont-ils liés ?

...

## 3. Expliquez le principe de réconciliation. Quelle composante Kubernetes est responsable de ce comportement ?

...

---

# Etape 3

## 1. Pourquoi ne peut-on pas simplement utiliser l’adresse IP du Pod calculator-calc pour permettre à un utilisateur d’accéder à l’application ?

...

## 2. Comment Kubernetes sait-il que le Service calculator-calc doit transmettre les requêtes au Pod de calculator-calc ?

...

## 3. Quelle est la différence entre le port exposé, le port cible et le NodePort utilisés dans votre architecture ?

...

---

# Etape 4

## 1. Pourquoi les quatre microservices utilisent-ils un port de type ClusterIP, tandis que calc-service utilise un port de type NodePort ?

...

## 2. comment Kubernetes permet-il au frontend de contacter le backend sans connaître l’adresse IP du Pod ?

...

## 3. On propose de configurer le frontend avec l’adresse IP actuelle des Pods backend (sum, sub...), par exemple "http ://10.x.x.x :<PORT>". Pourquoi cette solution n’est-elle pas adaptée à Kubernetes ?

...

