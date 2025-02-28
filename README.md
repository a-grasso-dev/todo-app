# TODO App

## Introduction
Ce projet est une application de gestion de tâches (To-Do List) développée avec **Spring Boot** pour le backend et **MongoDB** pour la base de données. L'interface utilisateur est construite avec **HTML**, **CSS** et **Javascript**. L'application permet d'ajouter, modifier, supprimer et lister des tâches.

## Outils et Technologies Utilisés
- **Backend :** Spring Boot (Java), Maven
- **Base de données :** MongoDB (MongoDB Atlas ou local via Docker)
- **Frontend :** **HTML**, **CSS** et **Javascript**
- **Docker :** Conteneurisation des services
- **GitHub :** Gestion du code source
---

## Lancer l'application depuis un shell Linux

### 1. Prérequis
- Avoir une connexion internet
- Installer Docker et Docker Compose

```sh
  sudo apt update && sudo apt install -y git docker docker-compose
```

### 2. Cloner le Projet
```sh
  git clone https://github.com/a-grasso-dev/todo-app.git
```

### 3. Depuis le dossier de l'application
```sh
  cd todo-app
```

### 4. Lancer docker-compose (en arrière-plan)
```sh
  sudo docker-compose up -d
```

### 5. Accéder à l’Application depuis l'interface
- **Frontend (interface utilisateur) :** [http://localhost](http://localhost)
- **Backend (API Spring Boot) :** [http://localhost:8080/api/tasks](http://localhost:8080/api/tasks)

### 6. Utilisation en Ligne de Commande

#### 6.1 Effectuer des requêtes API

- **Lister les tâches :**
```sh
  curl http://localhost:8080/api/tasks
```

- **Ajouter une tâche :**
```sh
  curl -X POST http://localhost:8080/api/tasks -H "Content-Type: application/json" -d '{"title": "Acheter du pain", "completed": false}'
```

- **Supprimer une tâche :**
```sh
  curl -X DELETE http://localhost:8080/api/tasks/{id}
```

#### 6.2 Accéder à la BDD MongoDB

- **Ouvrir un shell MongoDB :**
```sh
  sudo docker exec -it todo-app_mongodb_1 mongosh
  use todo_db
```

- **Afficher les tâches stockées dans la BDD :**
```sh
  db.tasks.find().pretty()
```

### 7. Arrêter l'application
```sh
  docker-compose down 
```
---

## Gestion des Erreurs

### "no space left on device"
- Supprimer les images, les conteneurs arrêtés et les volumes non utilisés
```sh
  docker system prune -a
 ```
- Supprimer des images Docker spécifiques si nécessaire
    - **Lister les images :**
```sh
  docker images
 ```
  - **Supprimer des images spécifiques :**
```sh
  docker rmi <image_id>
 ```
- Si l’erreur persiste, libérer de l’espace disque
```sh
  df -h
 ```
---
### "failed to bind host port for 0.0.0.0:80: address already in use"
- Voir quel processus utilise le port 80
```sh
  sudo netstat -tulnp | grep :80
```
- Si un serveur web comme Apache ou Nginx utilise le port 80, arrêtez-le temporairement
```sh
  sudo systemctl stop apache2
  sudo systemctl stop nginx
 ```

---

## Liens entre Frontend, Backend, API et BDD
- **Frontend (HTML/CSS/JS)** ➔ Appelle l'API REST via des requêtes HTTP.
- **Backend (Spring Boot)** ➔ Expose des endpoints REST (`/tasks` pour CRUD).
- **Base de données (MongoDB)** ➔ Stocke les tâches sous forme de documents JSON.
- **API REST** :
    - `GET /tasks` : Récupérer toutes les tâches
    - `POST /tasks` : Ajouter une tâche
    - `DELETE /tasks/{id}` : Supprimer une tâche

---

## Auteur
**Andrea GRASSO** - [GitHub](https://github.com/a-grasso-dev)\
_LP DEVOPS - IUT Lyon 1_\
_2024 / 2025_


