# Swagger-jsdoc

**Documentation Officielle :** https://www/npmjs.com/package/swagger-jsodc

**Vue d'ensemble :** https://swagger.io/docs/

## Introduction

**swagger-jsdoc** est une bibliothèque qui facilite la génération automatique de documentation API en utilisant les commentaires dans votre code source. Cette documentation respecte le standard OpenAPI, garantissant la compatibilité avec de nombreux outils tiers et plateformes.

## Fonctionnalités :

1. **Standardisation :** Produit des documents JSON ou YAML respectant la norme OpenAPI.
2. **Automatisation :** Evite de maintenir une documentation manuelle, souvent source d'erreurs.
3. **Flexibilité :** Compatible avec n'importe quel framework Node.js(Express, Koa, etc.)
4. **Support des définitions avancées :** Vous pouvez documenter les schémas de vos réponses et de vos paramètres, offrant une vue détaillée de l'API.

## Inconvénients potentiels :

- Ajoute un peu de complexité au code si les commentaires ne sont pas bien structurés.
- Nécessite une bonne compréhension des spécifications OpenAPI pour des cas complexes.

## Conclusion

**swagger-jsdoc** est un outil essentiel pour générer une documentation standardisée et professionnelle pour vos APIs. Il est particulièrement adapté aux équipes souhaitant collaborer efficacement et offrir une transparence totale aux développeurs tiers utilisant l'API.

### Exemple d'utilisation :

```bash
npm install swagger-jsdoc
```

### Configuration :

```js
const swaggerJsdoc = require('swagger-jsdoc');

const swaggerOptions = {
    definition; {
        openapi: '3.0.0',
        info: {
            title: 'API REST',
            version: '1.0.0',
            description: 'Documentation de l\'API REST',
        },
    },
    apis: ['./routes/*.js'], // Chemin vers vos fichiers où se trouvent les commentaires Swagger
};

const swaggerSpec = swaggerJsdoc(swaggerOptions);
module.exports = swaggerSpec;
```

### Commentaires Swagger dans vos fichiers de routes :

```js
/**
 * @swagger
 * /users:
 *   get:
 *     summary: Récupère la liste des utilisateurs
 *     responses:
 *       200:
 *         description: La liste des utilisateurs
 */
app.get('/users', (req, res) => {
    res.json([{ id: 1, username: 'JohnDoe' }]);
});
```