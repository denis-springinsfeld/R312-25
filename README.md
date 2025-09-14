# Sujet d'intégration : Portfolio Développeur avec Style Guide

## Objectif

Réaliser l'intégration d'un portfolio de développeur en respectant un style guide basé sur des tokens sémantiques CSS et la gestion de thèmes (clair/sombre).

## Livrables attendus

- Un site portfolio responsive (HTML/CSS, Tailwind)
- Un fichier **CSS configuration de TailwindCss** avec des variables sémantiques (tokens)
- Un mode clair et un mode sombre (via classes `.light` et/ou `.dark`)

## Style Guide

### Couleurs

```css
/* Primitive Tokens */
--clr-white: oklch(1 0 0);

--clr-gray-300: oklch(87.2% 0.01 258.338);
--clr-gray-400: oklch(70.7% 0.022 261.325);
--clr-gray-800: oklch(27.8% 0.033 256.848);
--clr-gray-900: oklch(21% 0.034 264.665);

--clr-green: oklch(87.1% 0.15 154.449);
--clr-green-300: oklch(79.2% 0.209 151.711);
```

### Typographie

- Police principale : 'Space Grotesk', sans-serif
- Textes : gras, tailles variables selon le breakpoint

---

## Déployer votre projet sur Github Pages

[cf doc](https://vite.dev/guide/static-deploy.html)

1. Créez un **dépôt GitHub** et poussez votre code.

2. Créer un répertoire `.github/workflows/deploy.yml` à la racine de votre projet.

3. Ajoutez le contenu suivant à `deploy.yml` :

```yaml
# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets the GITHUB_TOKEN permissions to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5
      - name: Set up Node
        uses: actions/setup-node@v4
        with:
          node-version: lts/*
          cache: "npm"
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
        with:
          # Upload dist folder
          path: "./dist"
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

4. Modifier le fichier `vite.config.ts` pour ajouter la base de votre projet (le nom du dépôt) :

```ts
import { defineConfig } from "vite";
import tailwindcss from "@tailwindcss/vite";
export default defineConfig({
  plugins: [tailwindcss()],
  base: "/<Nom du dépôt>",
});
```

5. Dans Github aller dans **Setting > Pages > Source > sélectionner `GitHub Actions`** et sauvegarder.

6. Pousser vos modifications sur la branche `main`. Le **workflow GitHub Actions** va se déclencher automatiquement et déployer votre site sur GitHub Pages à l'adresse :`https://<votre-nom-utilisateur>.github.io/<nom-du-depot>/`

Vous pouvez vérifier le statut du déploiement dans l'onglet **Actions** de votre dépôt GitHub.
