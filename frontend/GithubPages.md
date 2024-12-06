# Déploiement d'un projet React sur GitHub Pages

## Préparer le projet

1. Initialiser un projet React :

```bash
npx create-react-app mon-projet
cd mon-projet
```

2. S'assurer que le dépôt est lié à GitHub :

- Crée un dépôt sur GitHub
- Relie le dépôt local au dépôt distant

```bash
git init
git remote add origin https://github.com/<ton-username>/mon-projet.git
git branch -M main
git push -u origin main
```

## Installer `gh-pages`

1. Installer la dépendance `gh-pages` :

```bash
npm install gh-pages --save-dev
```

##Modifier le fichier `package.json`

1. Ouvre le fichier `package.json`.
2. Ajoute ou modifie les champs suivants :
    - `homepage` : Ajoute l'URL de ton site GitHub Pages :
```bash
"homepage": "https://<ton-username>.github.io/<nom-du-repo>"
```

    - `scripts` : Ajoute la commande de déploiement :
```bash
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

## Déployer le projet

1. Construis et déploie le projet avec une seule commande :

```bash
npm run deploy
```

- Le script `predeploy` génère le dossier `build`.
- Le script `deploy` déploie le contenu du dossier `build` sur la branche `gh-pages`.

## Configurer GitHub Pages

1. Accède à **Setting -> Pages** dans ton dépôt GitHub.
2. Dans la section **Source**, sélectionne la branche `gh-pages`, si cela n'est pas déjà fait.
3. Clique sur **Save**.

## Vérifier le site

- Va sur l'URL de ton site (indique dans le champ `homepage`).
- Si le site ne s'affiche pas immédiatement, attends quelques minutes.

# Commandes utiles pour maintenance

## Mettre à jour le site

- Lorsque tu modifies ton projet, exécute simplement :
```bash
npm run deploy
```

## Supprimer la branche `gh-pages` (si nécessaire)

- Si tu veux reportir de zéro ou résoudre un problème :
```bash
git branch -D gh-pages
git push origin --delete gh-pages
```

# Points à vérifier en cas de problème

1. **Le champs `homepage` dans `package.json`**:
    - Vérifie qu'il contient la bonne URL de ton site.
2. **Les commandes `npm install` et `npm run build`**:
    - Assure-toi qu'elles n'ont pas d'erreurs.
3. **Le cache du navigateur**:
    - Si le site ne se met pas à jour, vide le cache ou force le rafraîchissement(`Ctrl + F5`/`Cmd + Shift + R`)