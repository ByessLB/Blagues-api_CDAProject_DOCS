# Conception du projet "Mini Application web de Blagues" - Carambar & Co

## Architecture générale

### Backend (API)

- **Langage/Framework :** Node.js avec Express.js
- **Base de données :** SQLite géré via Sequelize (ORM).
- **Approche MVC :**
    - **Model :** Gestion des blagues (modèle Sequelize).
    - **View :** API exposée via JSON (pas de templates pour cette API).
    - **Controller :** Logique métier pour manipuler les blagues.

### Frontend

- **Technologies :** HTML, CSS, JavaScript (Vanilla ou Vue.js)
- **Hébergement :** GitHub Pages.
- **Fonctionnalités :** 
    - Une landing page simple avec un bouton pour afficher une blague aléatoire.
    - Appels à l'API backend pour récupérer les données.

## Fonctionnalités demandées et spécifications

### Backend

| **Fonctionnalité** | **Description** | **Endpoint** |
| :---: | :---: | :---: |
| Ajouter une blague | Permet d'insérer une nouvelle blague dans la base de données via un appel POST. | `POST /blagues` |
| Consulter toutes les blagues | Retourne une liste de toutes les blagues stockées. | `GET /blagues` |
| Consulter une blague par ID | Permet de récupérer une blaque précise via son ID. | `GET /blagues/:id` |
| Consulter une blague aléatoire | Retourne une blague aléatoire. | `GET /blagues/random` |

### Frontend

| **Fonctionnalité** | **Description** |
| :---: | :---: |
| Landing page | Une page simple et design représentant Carambar & Co, avec un bouton pour afficher une blague. |
| Récupération aléatoire de blagues | Appels à l'API backend via le bouton afficher des blagues aléatoires. |
