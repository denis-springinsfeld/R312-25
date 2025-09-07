# R3.12

## Tailwind CSS 4

[installation](https://tailwindcss.com/docs/installation/using-vite)

```shell
# Installation du projet Vite dans le dossier courant - choisir React JS
npm create vite@latest .

# Installation de TailwindCSS
npm install tailwindcss @tailwindcss/vite
```

- Modifier votre structure de projet

```shell
/TD2-TailwindCSS
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

- Configure the Vite plugin en créant un fichier `vite.config.js` :

```js
// vite.config.js
import { defineConfig } from "vite";
import tailwindcss from "@tailwindcss/vite";
export default defineConfig({
  plugins: [tailwindcss()],
});
```

- Ajouter Prettier :
  [doc](https://tailwindcss.com/docs/editor-setup#class-sorting-with-prettier)

```shell
npm install -D prettier prettier-plugin-tailwindcss
```

- Ajouter la configuration Prettier :

```js
// .prettierrc
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

- Installation de l'extension Tailwind CSS IntelliSense dans VSCode

- Modifier le fichier `index.html` :

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link href="/src/style.css" rel="stylesheet" />
  </head>
  <body>
    <h1 class="text-3xl font-bold underline">Hello world!</h1>
  </body>
</html>
```

- Modifier le fichier `style.css` :

```css
@import "tailwindcss";
```

## Exercice :

### 1 Créer une carte Call to Action avec TailwindCSS en utilisant les classes de base.

![image](doc/Exo1_S.png)
![image](doc/Exo1_M.png)

```html
<!-- Card Component -->
<article class="">
  <h2 class="">
    Focus on your content.
    <br />
    We handle the distribution.
  </h2>
  <p class="">
    Ac euismod vel sit maecenas id pellentesque eu sed consectetur. Malesuada
    adipiscing sagittis vel nulla nec.
  </p>
  <div class="">
    <a href="#" class=""> Get started </a>
    <a href="#" class=""> Live demo </a>
  </div>
</article>
```

### 2 Configuration des Variables CSS dans le fichier `index.css`

- Ajoutez la directive `@theme` et modifiez la couleur que vous avez utilisée dans la carte : `--color-blue-500`

- Ajoutez une variable `--background-image-bgImage` et utilisez cette variable pour définir une image de fond dans la carte.

```css
@import "tailwindcss";

@theme {
  /* Déclaration de variables CSS dans le thème permet de générer également les classes utilitaires : bg-bgImage, et utilisez cette variable pour définir une image de fond dans la carte. */
  --color-blue-500: #f6893bff;
  /* Crée une classe utilitaire pour l'image de fond, propriété css background-image */
  --background-image-bgImage: linear-gradient(
      to top,
      --alpha(var(--color-blue-500) / 1),
      --alpha(var(--color-blue-500) / 0.75)
    ), url("/src/assets/bg-image.jpg");
}
```

- Créer des thèmes colorés simplement en utilisant les variables CSS

```css
@import "tailwindcss";

@theme inline {
  /* Déclaration de variables CSS dans le thème permet de générer également les classes utilitaires : bg-background, text-background... */
  --color-background: var(--background);
  --color-foreground: var(--foreground);
}

@layer base {
  :root {
    /* Tokens Primitives */

    /* Format OKLCH: Lightness Chroma Hue */
    /* L: 0-1 (0=noir, 1=blanc) */
    /* C: 0-0.4 (0=gris, plus élevé=plus saturé) */
    /* H: 0-360 (teinte en degrés) */

    --clr-light: oklch(1 0 0);
    --clr-dark: oklch(0 0 0);

    /* Tokens Sémantiques */
    --background: var(--clr-light);
    --foreground: var(--clr-dark);
  }

  .dark {
    --background: var(--clr-dark);
    --foreground: var(--clr-light);
  }
}
```

- Sur ce modèle, créez des thèmes Red, Neon ...

![](doc/Exo_Final.png)
