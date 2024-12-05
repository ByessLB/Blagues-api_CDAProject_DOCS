# SQLite

**Documentation Officielle :** https://sqlite.org/docs.html

**Documentation du package :** https://www.npmjs.com/package/sqlite3

## Introduction

SQLite est une base de données relationnelle légère, autonome et intégrée. Contrairement aux systèmes de gestion de base de données (SGBD) traditionnels comme MySQL ou PostgreSQL, SQLite ne nécessite pas de serveur poru fonctionner. Les données sont stockées dans un fichier unique sur le disque, ce qui rend SQLite particulièrement adapté aux petit projets, aux applications mobiles ou aux outils de prototypage.

### Caractéristiques principales

- **Léger :** Pas de serveur ni de processus dédié
- **Portable :** Tout est contenu dans un fichier unique
- **Open Source :** Gratuit et sous licence publique
- **Performant :** Suffisamment rapide pour une majorité de cas d'utilisation
- **Compatible :** Supporte les fonctionnalités SQL standard(CRUD, JOIN, etc.)

### Cas d'utilisation

- Application mobiles (iOS, Android)
- Prototypes et petits projets
- Stockage de données embarqu" dans des applications
- Solutions où un système de base de données autonome est nécessaire

## Utilisation de SQLite avec Node.js

Pour intégrer SQLite dans un projet Node.js, on utilise généralement le package `sqlite3`.

### Installation

Pour installer `sqlite3`, exécutez la commande suivante dans votre terminal:

```bash
npm install sqlite3
```

### Configuration

Voici comment configurer SQLite dans votre projet Node.js:

1. Importer sqlite3

```js
const sqlite3 = require('sqlite3').verbose();
```

2. Créer une connexion à la base de données

La base de données sera stockée dans un fichier (`database.sqlite`)

```js
const db = new sqlite3.Database('./database.sqlite', (err) => {
    if (err) {
        return console.error('Erreur lors de la connexion à la base de données :' err.message);
    }
    console.log('Connexion à la base de données réussie.');
});
```

3. Créer une table

Exemple de création d'une table `blagues` :

```js
db.run(`
    CREATE TABLE IF NOT EXISTS blagues (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    question TEXT NOT NULL,
    reponse TEXT NOT NULL
  )`
, (err) => {
    if (err) {
        console.error('Erreur lors de la création de la table :', err.message);
    } else {
        console.log('Table créée avec succès.');
    }
});
```

4. Ajouter des données

Exemple pour insérer une blague dans la base :

```js
const question = "Quelle est la femelle du hamster ?";
const reponse = "L'Amsterdam";

db.run(`INSERT INTO blagues (question, reponse) VALUES (?, ?)`, [question, reponse], function(err) {
  if (err) {
    return console.error('Erreur lors de l\'insertion :', err.message);
  }
  console.log(`Blague ajoutée avec l'ID : ${this.lastID}`);
});
```

5. Récupérer des données

Exemple de récupération des blagues :

```js
db.all(`SELECT * FROM blagues`, [], (err, rows) => {
  if (err) {
    throw err;
  }
  rows.forEach((row) => {
    console.log(`${row.id} : ${row.question} - ${row.reponse}`);
  });
});
```

6. Fermeture de la connexion

Il est important de fermer la connexion à la base de données lorsque l'application s'arrête.

```js
db.close((err) => {
  if (err) {
    return console.error('Erreur lors de la fermeture de la base de données :', err.message);
  }
  console.log('Connexion à la base de données fermée.');
});
```

## Avantage et inconvénients de SQLite

### Avantages

- **Facilité d'utilisation :** Pas de configuration complexe
- **Autonome :** Aucune installation de serveur nécessaire
- **Portable :** Le fichier peut être déplacé facilement
- **Rapide :** Performant pour de petites bases de données.

### Inconvénients

- **Non adapté aux grandes base de données :** Moins performant que MySQL ou PostgreSQL pour de très gros volumes de données
- **Pas multi-utilisateur :** Moins adapté pour des applications à forte concurrence
- **Pas de fonctionnalités avancées :** Certaines fonctionnalités comme les permissions complexes sont limités
