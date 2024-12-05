# Swagger-ui-express

**Documentation Officielle :** https://www/npmjs.com/package/swagger-ui-express

**Vue d'ensemble :** https://swagger.io/docs/

## Introduction

**swagger-ui-express** complète **swagger-jsdoc** en permettant d'afficher et d'intéragir avec la documentation API générée via une interface graphique. Cette interface rend les APIs accessibles même à des non-développeurs, comme des chefs de projet ou des testeurs.

## Fonctionnalités :

1. **Intégration :** directe avec Express.
2. **Interactivité :** les utilisatuers peuvent tester directement les endpoints via une interface web intuitive.
3. **Simplicité d'intéfration**: en quelques ligne de code, vous pouvez exposer la documentation sur une URL dédiée.
3. **Amélioration de l'expérience développeur :** Les développeurs peuvent explorer rapidement les endpoints disponibles et comprendre les paramètres attendus.

## Inconvénients potentiels :

- Non adapté aux applications nécessitant une documentation offline ou statique.
- Dépend fortement de la qualité des spécifications fournies par swagger-jsdoc.

## Conclusion

**swagger-ui-express** est l'outil parfait pour fournir une documentation claire et testable aux développeurs et utilisateurs finaux de votre API. Associé à **swagger-jsdoc**, il devient un atout clé pour toutes API professionnelle.

### Exemple d'utilisation :

```bash
npm install swagger-ui-express
```

### Mise en place avec Express :

```js
const express = require('express');
const swaggerUi = require('swagger-ui-express');
const swaggerSpec = require('./swaggerSpec'); // Importer la configuration swagger-jsdoc. Une interface graphique est générée à partir de cette configuration.

const app = express();
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec)); // Définir la route pour l'interface Swagger. Le paramètre `serve` est utilisé pour servir la documentation, tandis que `setup ` est utilisé pour configurer l'interface. 


app.listen(3000, () => {
    console.log('Le serveur est lancé sur http://localhost:3000');
    console.log('Documentation Swagger disponible sur http://localhost:3000/api-docs');
});
```