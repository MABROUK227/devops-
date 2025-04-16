Rental Service Application

Description

L'application Rental Service permet aux utilisateurs de consulter les voitures disponibles, de louer une voiture en spécifiant des dates de début et de fin, et de réinitialiser une location. Cette application utilise Node.js, Express, Docker, et Kubernetes pour la gestion du backend, ainsi qu'un frontend simple en HTML, CSS, et JavaScript.

Installation

1. Clonez le repository
Clonez le repository depuis GitHub :

git clone https://github.com/MABROUK227/devops-.git
cd devops-
2. Installez les dépendances
Naviguez dans le répertoire /app et installez les dépendances nécessaires :

cd app
npm install
3. Lancer l'application localement
Lancer le serveur Node.js :

npm start
Une fois l'application lancée, ouvrez votre navigateur et allez à http://localhost:4000 pour accéder à l'interface frontale.

4. Déploiement avec Docker
Construire l'image Docker :

docker build -t rentalservice .
Exécuter le conteneur Docker :

docker run -p 4000:4000 rentalservice
Ensuite, ouvrez votre navigateur et allez à http://localhost:4000 pour accéder à l'interface via Docker.

5. Déploiement avec Kubernetes
Assurez-vous d'avoir kubectl et Istio installés et configurés.

Déployer le service dans Kubernetes :

kubectl create deployment rentalservice --image=mabrouk148/rentalservice:1.0.0
Déployez ensuite le service en utilisant un fichier deployment.yaml :

kubectl apply -f deployment.yaml
Créez la gateway Istio :

kubectl -n istio-system port-forward deployment/istio-ingressgateway 31380:8080
Ensuite, ouvrez votre navigateur et allez à http://localhost:31380 pour accéder à l'interface via la gateway Istio.

Endpoints d'API

L'application expose plusieurs points d'API pour interagir avec les données des voitures.

1. GET /api/cars : Récupérer toutes les voitures
Récupère la liste de toutes les voitures disponibles.

Réponse :

Code 200 : Liste des voitures en format JSON.
Code 500 : Erreur serveur.
2. GET /api/cars/:numberPlate : Récupérer une voiture spécifique par son numéro d'immatriculation
Récupère les détails d'une voiture en fonction de son numéro d'immatriculation.

Paramètres :

numberPlate : Le numéro d'immatriculation de la voiture.
Réponse :

Code 200 : Détails de la voiture en format JSON.
Code 404 : Voiture non trouvée.
Code 500 : Erreur serveur.
3. PUT /api/cars/:numberPlate : Mettre à jour les dates de location d'une voiture
Permet de mettre à jour les dates de location d'une voiture identifiée par son numéro d'immatriculation.

Paramètres :

numberPlate : Le numéro d'immatriculation de la voiture.
Body : Les nouvelles dates de location (date de début et de fin).
Réponse :

Code 200 : Détails de la voiture mise à jour en format JSON.
Code 404 : Voiture non trouvée.
Code 500 : Erreur serveur.
Déploiement Kubernetes (Fichier deployment.yaml)

Voici un exemple de fichier deployment.yaml pour déployer l'application dans Kubernetes.

apiVersion: apps/v1
kind: Deployment
metadata:
  name: rentalservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: rentalservice
  template:
    metadata:
      labels:
        app: rentalservice
    spec:
      containers:
        - name: rentalservice
          image: mabrouk148/rentalservice:1.0.0
          ports:
            - containerPort: 4000
Conclusion

Ce guide vous permet de déployer l'application Rental Service localement, avec Docker, ou dans un cluster Kubernetes. Vous pouvez utiliser les endpoints API pour interagir avec les voitures disponibles et gérer les locations.

Pour toute question ou contribution, n'hésitez pas à ouvrir un issue ou une pull request.