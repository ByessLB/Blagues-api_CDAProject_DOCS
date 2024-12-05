# Sequelize

**Documentation Officielle :** https://sequelize.org/

## Introduction

Sequelize est un ORM (Object Relationnal Mapper) conçu pour simplifier la gestion des bases de données relationnelles dans une application Node.js. Contrairement à l'approche traditionnelle où on utilise des requêtes SQL brutes (CRUD), Sequelize permet de manipuler la base via des objets JavaScript, rendant la code plus lisible et structuré.

## Fonctionnalités :

1. **Abstraction des bases de données :** Vous pouvez changer de base de données (MySQL, PostgrSQL, SQLite, MariaBD) sans modifier profondément votre code.
2. **Support des relations complexes :** Sequelize gère facilement les relations entre table (One-to-One, One-to-Many, Many-to-Many).
3. **Validation et hooks :** Des mécanismes comme les validations automatiques et les hooks permettent de contrôler le cycle de vie des modèles (ex: avant la sauvegarde).
4. **Système de migrations :** Il permet de versionner et de gérer les modifications dans les structures des tables (ajout de colonnes, suppression, etc.).

## Inconvénients potentiels :

- Courbe d'apprentissage : la syntaxe de Sequelize peut être complexe pour les débutants.
- Moins performant sur les requêtes très complexes par rapport à des requêtes SQL directes.

## Conclusion

Sequelize est un outil puissant pour gérer zdes bases de données relationnelles avec Node.js. Il est idéal pour les projets où la simplicité et la maintenabilité du code sont prioritaires. Cependant, pour des applications critiques où les performances de requêtes sont essentielles, il peut être nécessaire de combiner Sequelize avec des reuqêtes SQL brutes pour des cas spécifiques.

### Exemple d'utilisation :

```bash
npm install sequelize sqlite3
```

### Initialisation

```js
const { sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('database', 'username', 'password', {
    host: 'localhost',
    dialect: 'sqlite', // ou 'postgres', 'mysql', etc.
});

// Test de connexion
(async () => {
    try {
        await sequlize.authenticate();
        console.log('Connexion réussie à la base de données.');
    } catch (error) {
        console.error('Erreur de connexion : ', error);
    }
})();
```

### Définition d'un modèle

```js
const User = sequelize.define('User', {
    id: {
        type: DataTypes.INTEGER,
        primaryKey: true
    },
    username: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    email: {
        type: DataTypes.STRING,
        unique: true,
        allowNull: false,
    },
});

// Synchonisation du modèle
(async () => {
    await sequelize.sync({ force: true });
    console.log('Les modèles sont synchonisés.');
})();
```