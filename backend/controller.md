# Controller

## Méthodes

### Méthodes `async` et `await`

**Définition**

Les mots-clés `async` et `await` sont utilisés pour gérer des opérations asynchrones dans JavaScript.

- `async` est utilisé pour définir une fonction asynchrone, qui retourne toujours une **promesse**
- `await` est utilisé à l'intérieur des fonctions `async` pour attendre que la promesse soit résolue ou rejetée.

**Exemple**

```js
const blague = await Blague.create(req.body);
```

ici :
- `await` suspend l'exécution jusqu'à ce que la méthode `Blague.create()` ait terminé.
- Si `Blague.create()` réussit, la valeur de retour est assignée à `blague`
- Si elle échoue, une erreur est générée.

L'utilisation de `async/await` rend le code plus lisible que les chaînes de `.then()` et `.catch()` utilisées avec des promesses.

### Gestion des erreurs avec `try/catch`

**Définition**

Le bloc `try-catch` est utilisé pour gérer les erreurs qui peuvent se produir dans le code
- `try`: Le code susceptible de générer une erreur est placé ici.
- `catch`: Ce bloc capture et traite toute erreur levée dans le bloc `try`

**Exemple**

```js
try {
    cont blague = await Blague.create(req.body);
    res.status(201).json(blague);
} catch (error) {
    res.status(500).json({ error: 'Erreur lors de l\'ajout de la blague.' });
};
```

- Si une erreur se produit dans `Blague.create(req.body)`, elle est capturé dans le bloc `catch`
- La méthode `res.status(50).json()` envoie une réponse avec un code erreur HTTP 500 (Erreur interne du serveur)

### Séparation des responsabilités

Chaque méthode du contrôleur gère une tâche spécifique :

- `ajouterBlague` : Ajouter une nouvelle blague à la base de données
- `toutesBlagues`: Récupérer toutes les blagues
- `uneBlague`: Récupère une blague spécifique par son ID
- `blagueAleatoire`: Récupère une blague aléatoire

Cette séparation suit le principe de **Single Responsibility Principle (SRP)**, rendant le code plus modulaire et facile à maintenir

### Interaction avec Sequelize

**Sequelize**

Sequelize est un ORM (Object-Relational Mapping) pour Node.js. il permet d'interagir avec des bases de données relationnelles en utilisant du JavaScript au lieu du SQL brut.

- **Méthodes utiliées :**

    - `Blague.create(req.body)`: Insère un nouvel enregistrement dans la table
    - `Blague.findAll()`: Récupère tous les enregistrements
    - `Blague.findByPk(id)`: Récupère un enregistrement spécifique par sa clé primaire
    - `Blague.findOne({ order: sequelize.random() })`: Récupère un seul enregistrement, ici aléatoirement grâce à `sequelize.random()`

### Gestion des réponses HTTP

- `res.status(code).json(data)`
    - `res.status(201).json(blague)`: Répond avec un statut 201 (Crée) et retourne l'objet ajouté.
    - `res.status(500).json({ error: 'Erreur ...' })`: Répond avec un statut 500 pour signaler une erreur interne

- **Exemple**

```js
if (!blague) {
    res.status(404).json({ error: 'Blague non trouvée' });
}
```
`404` est utilisé pour indiquer que la ressource n'existe pas.

### Requête aléatoire avec `sequelize.random()`

```js
const blague = await Blague.findOne({ order: sequelize.random() });
```
Ici, `sequeliza.random()` permet de récupérer un enrefistrement aléatoire. Sequeliza utilise des fonctions SQL spécifiques (`RAND()` ou `RANDOM()`, selon la base de données)

### Résumé des concepts clés

| Concept | Description |
| --- | --- |
| `async/await` | Gère les opérations asynchrones de manière lisible. |
| `try/catch` | Gère les erreurs et les exceptions. |
| `Sequelize` | ORM pour interagir avec des bases de données relationnelles |
| Status HTTP | Indique si la requête a réussi ou a échoué (`201`,`500`,`404`) |
| Méthodes CRUD | Create, Read, Update, Delete, Organisées en méthodes |