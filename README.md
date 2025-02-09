# eslint-oi-nuxt-rules

## Description

`eslint-oi-nuxt-rules` est un ensemble de règles ESLint conçu pour les projets Nuxt.js utilisant Vue et Pug, basé sur la configuration d'Airbnb. Il simplifie l'intégration de règles de linting robustes et modernes dans vos projets.

---

## Installation

### Étape 1 : Pré-requis

Avant d'installer `eslint-oi-nuxt-rules`, il est nécessaire d'installer les packages suivants :

```bash
npm install eslint eslint-config-airbnb-base eslint-plugin-vue-pug @eslint/eslintrc @nuxt/eslint --save-dev
```

### Étape 2 : Installer eslint-oi-nuxt-rules

Installez la dépendance :

```bash
npm install git+ssh://git@bitbucket.org:proprietes-privees/eslint-oi-nuxt-rules --save-dev
```

### Étape 3 : Configurer ESLint

Lancez l'initialisation d'ESLint pour configurer votre projet :

```bash
npx eslint --init
```

Répondez aux questions suivantes :

1. How would you like to use ESLint?
    * ➡️ To check syntax and find problems

2. What type of modules does your project use?
    * ➡️ JavaScript modules (import/export)

3. Which framework does your project use?
    * ➡️ Vue.js

4. Does your project use TypeScript?
    * ➡️ No

5. Where does your code run?
    * ➡️ Browser

6. Would you like to install them now?
    * ➡️ Yes

### Étape 4 : Configurer Nuxt

Ajoutez la configuration suivante dans le fichier nuxt.config.ts :

```javascript
export default defineNuxtConfig({
  // ...
    eslint: {
      config: {
        standalone: false
      }
    },
    modules: [
      '@nuxt/eslint', // https://eslint.nuxt.com/packages/module
      // ...
    ],
    // ...
})
```

### Étape 5 : Configurer eslint.config.js

Ajoutez la configuration suivante dans le fichier eslint.config.js :

```javascript
import globals from 'globals';
import pluginJs from '@eslint/js';
import pluginVue from 'eslint-plugin-vue';
import { vuePugConfig, airBnbConfig, customConfig } from 'eslint-oi-nuxt-rules';
import { withNuxt } from './.nuxt/eslint.config.mjs';

/** @type {import('eslint').Linter.Config[]} */
export default withNuxt([
  { files: ['**/*.{js,mjs,cjs,vue}'] },
  { languageOptions: { globals: globals.browser } },
  ...airBnbConfig,
  pluginJs.configs.recommended,
  ...pluginVue.configs['flat/recommended'],
  ...vuePugConfig,
  ...customConfig,
]);
```

### Étape 6 : Ajouter un script npm

Ajoutez le script suivant dans votre fichier package.json :

```json
{
  "scripts": {
    "lint:js": "eslint ."
  }
}
```

---

## Utilisation

Pour vérifier votre code avec ESLint, lancez simplement :

```bash
npm run lint:js
```

Vous pouvez aussi utiliser une extension eslint pour votre IDE.
