# TD1 Sass - R3.12 2025/2026

## A\_ Initialisation du projet

### 💻 A_1 Initialisez votre projet :

- Créer un dossier `TD1_sass`,
- Ouvrir ce dossier dans votre éditeur de code,
- Ouvrir le terminal et initialiser un projet [`Vite js`](https://vitejs.dev/guide/)

```shell
# Initialiser le projet
npm create vite@latest

# Répondre aux questions
◇  Project name:
│  . # le dossier dans lequel vous travaillez
◇  Package name:
│  td1_sass # le nom de votre package identique au dossier
◇  Select a framework:
│  Vanilla # le framework que vous utilisez
◇  Select a variant:
│  Javascript # Javascript simplement

# Installer les dépendances
npm install

```

- Structure de votre `dossier de travail`

```shell
/TD1-sass
  /public
    vite.svg ❌
  /src
    counter.js ❌
    javascript.js ❌
    main.js ❌
    style.css
  index.html
  package.json

```

- Modifier le fichier `index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>TD1_SASS</title>
    <link rel="stylesheet" href="src/style.css" />
  </head>
  <body>
    <h1>Hello <em>World</em>Vite!</h1>
  </body>
</html>
```

```css
body {
  font-family: sans-serif;
  font-size: 2rem;
  background: hsl(226, 19%, 58%);
  color: hsl(0, 0%, 20%);
}
```

### 💻 A_2 run dev et run build :

Lancer le serveur de développement

```shell
# Lancer le serveur de développement
npm run dev
```

Un serveur de développement Vite devrait maintenant être en cours d'exécution.

Pour vérifier le fonctionnement, ouvrez votre navigateur et accédez à `http://localhost:5173`.

Pour suspendre le serveur, utilisez `Ctrl + C` dans le terminal.

Attention vous travaillez sur **un projet en développement**.
Pour construire le projet, exécutez la commande suivante :

```shell
# Suspendre le serveur
# Construire le projet
npm run build
```

Un dossier `dist` devrait être créé à la racine de votre projet. Celui-ci contiendra les **fichiers optimisés pour la production**. Regardez le contenu de ce dossier pour voir les fichiers générés.
Votre CSS devrait être compilé en CSS standard et minifié.
Pour ce TD nous allons modifier la configuration de Vite pour obtenir un fichier CSS non minifié.

Créer à la racine du projet un fichier `vite.config.js` avec le contenu suivant :

```javascript
import { defineConfig } from "vite";

export default defineConfig({
  build: {
    minify: false, // Désactive la minification CSS/JS
    cssCodeSplit: false, // Un seul fichier CSS
  },
});
```

À présent effectuer un nouveau build de votre projet.

- Modifier le fichier `style.css` en `style.scss`
- Modifier le fichier `index.html` pour inclure le fichier `style.scss`
- Lancer le serveur de développement, une erreur devrait apparaître dans la console, indiquant que 'sass' n'est pas installé.

- Vous devez installer Sass en tant que dépendance de développement.

```shell
# Installer sass
npm install -D sass
```

- Relancer le serveur de développement,
- Tester quelques propriétés CSS.

- [ctrl + c]
- ReBuild le projet.

Rem : vous pouvez aussi ajouter `prettier` pour formater votre code.

```shell
# Installer prettier
npm install -D prettier
```

## B\_ EXERCICES

### 💻 Exercice 1 : Pur CSS dans un fichier SCSS

4 boutons : info, alert, warning et error avec la méthode BEM - un **Block** 'button' et 4 **Modifiers**.

Copier le code suivant dans votre fichier `index.html` :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>TD2</title>

    <link rel="stylesheet" href="/src/style.scss" />
  </head>
  <body>
    <div class="container">
      <a href="#" class="btn">Default</a>
      <a href="#" class="btn btn--info">Info</a>
      <a href="#" class="btn btn--success">Success</a>
      <a href="#" class="btn btn--warning">Warning</a>
      <a href="#" class="btn btn--error">Error</a>
    </div>
  </body>
</html>
```

Copiez le code suivant dans votre fichier `style.scss` :

```scss
/* Rubik Variable Font Face */
@font-face {
  font-family: "Rubik";
  src: url("/Rubik/Rubik-VariableFont_wght.ttf") format("truetype");
  font-weight: 100 900;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: "Rubik";
  src: url("/Rubik/Rubik-Italic-VariableFont_wght.ttf") format("truetype");
  font-weight: 100 900;
  font-style: italic;
  font-display: swap;
}

:root {
}

// ====================================
// Mini reset uniquement pour test
// https://piccalil.li/blog/a-more-modern-css-reset/
// ====================================

*,
*::after,
*::before {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

a,
a:active,
a:visited {
  text-decoration: none;
  cursor: pointer;
}

// ====================================
// Base
// ====================================

body {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  font-family: "Rubik", sans-serif;

  background-color: oklch(0.13 0.028 261.692);
}

// ====================================
// Layout
// ====================================

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

// ====================================
// Components
// ====================================

.btn {
  // Utilisation de variables CSS privée
  --_bg: oklch(1 0 0);

  display: inline-flex;
  justify-content: center;
  align-items: center;
  min-width: 10ch;
  min-height: 44px;
  padding: 0.8em 3em;

  color: oklch(0.3 0 0);
  text-transform: uppercase;
  line-height: 1rem;

  background-color: var(--_bg, oklch(1 0 0));
  box-shadow: 8px 8px 0 rgba(0, 0, 0, 0.5);
  border-radius: 20px;

  transition: all 0.3s ease-in-out;
}

.btn:hover {
  background-color: oklch(1 0 0 / 0.5);
}

// Variants

.btn--info {
  --_bg: oklch(0.7584 0.1373 231.6);
}
.btn--success {
  --_bg: oklch(0.7733 0.1523 163.3);
}
.btn--warning {
  --_bg: oklch(0.8334 0.1641 83.87);
}
.btn--error {
  --_bg: oklch(0.7123 0.1656 22.18);
}
```

### 💻 Exercice 2 : Sass

Vous devriez maintenant pouvoir utiliser Sass dans votre projet.

Modifier le fichier `style.scss` pour réécrire

- Sass et le nesting .

#### Exercice 2.1 : Variables

Ajoutez des `variables` Sass à votre code.
Regardez les fonctions de Sass pour modifier la couleur au survol de manière dynamique.
https://sass-lang.com/documentation/modules/color/

#### Exercice 2.3 : Maps et boucles

Simplifier votre code en utilisant une Map et une boucle `@each`.
https://sass-lang.com/documentation/at-rules/control/each

#### Exercice 2.4 : avec des variables CSS.

Reprendre votre travail en utilisant des variables CSS (custom properties).

En utilisant la `Maps` créer

```css
|  :root {
|       --clr-primary: 198 93% 60%;
        --clr-success: 158 64% 52%;
        --clr-warning: 43 96% 56%;
        --clr-error: 0 91% 71%;
    }
```

#### Exercice 2.5 : partials.

Réorganiser votre code en utilisant des `partials`.

https://sass-lang.com/guide#topic-4

### 💻 Exercice 3 : card

DS :
--font-family-primary: "Vollkorn", serif;
--font-family-primary: 'Vollkorn', serif;
--font-family-secondary: 'PT Sans', sans-serif;
--font-size-heading: 2rem;
--font-size-caption: 0.875rem;
--color-border: #34b897;
--color-text: #222022;
--color-highlight-primary: #FFEF7E;
--color-highlight-secondary: #B7F9E9;
--border-radius: 1.25rem;
--box: 10px;
