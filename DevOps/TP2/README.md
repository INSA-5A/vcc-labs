# Etape 1

## 1. Pourquoi est-il nécessaire que Jenkins puisse communiquer avec VM-K8s et VM-Registry ?

Jenkins doit communiquer avec VM-Registry pour publier les images Docker. Il doit accéder à l’API Kubernetes sur VM-K8s pour déployer et mettre à jour l’application automatiquement.

## 2. Quel est le rôle de Jenkins dans la chaîne CI/CD ?

Jenkins orchestre la chaîne CI/CD. Il récupère le code Git, lance le build et les tests, publie les images Docker puis déclenche leur déploiement sur Kubernetes.

---

# Etape 2

## 1. Quelles opérations réalisées manuellement dans le TP1 ont été automatisées par Jenkins ?

Jenkins automatise la récupération du code source et la build des cinq images Docker (pas la publication).

## 2. Votre pipeline comporte plusieurs étapes. Que se passe-t-il si la construction de l’image calculator-sub échoue ?

Si la construction de calculator-sub échoue, le pipeline est marqué en échec et les étapes suivantes sont interrompues par défaut. Les images déjà construites restent présentes, ainsi l'ancien service fonctionnel continue de tourner.

## 3. Le Webhook GitHub est la méthode la plus utilisée en entreprise dans une chaîne CI. Quelles opérations devriez-vous faire pour la mettre en place dans votre architecture ?

Pour utiliser un Webhook GitHub il faut :
- rendre Jenkins accessible depuis GitHub avec une URL publique
- autoriser le trafic dans OpenStack
- configurer dans GitHub un webhook vers https://<adresse-jenkins>/github-webhook/ pour les événements push
- activer le déclencheur GitHub hook trigger for GITScm polling dans le job Jenkins

---

# Etape 3

## 1. Pourquoi Jenkins doit-il disposer d’un accès à l’API Kubernetes ?

Jenkins doit accéder à l’API Kubernetes pour appliquer les manifestes avec kubectl apply. Cela lui permet de créer ou mettre à jour les Deployments et Services automatiquement.

## 2. Quelles étapes du job Jenkins correspondent à la CI, et lesquelles correspondent à la CD ?

La CI correspond à la récupération du code Git et au build des images Docker (et tests si existants). La CD correspond à leur publication dans le Registry et leur déploiement sur Kubernetes. 

## 3. Quel est le parcours d’une modification du code source depuis le "git push" jusqu’à l’application Calculator ? Pour chaque étape, indiquez l’outil ou la technologie qui intervient.

Le parcours d’une modification est le suivant :
- Git/GitHub : le développeur push son commit avec git push.
- Jenkins : le polling détecte le changement et déclenche le pipeline.
- Docker : Jenkins construit les cinq images puis les publie dans le Registry.
- kubectl/API Kubernetes : Jenkins applique les manifestes de déploiement.
- Kubernetes : si la référence de l’image a changé dans le Deployment, il remplace progressivement les Pods par ceux utilisant la nouvelle version.

