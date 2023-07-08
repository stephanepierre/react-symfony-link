## INSTALLATION
- symfony new (nom du projet) --webapp
- cd (nom du projet)
- composer require symfony/webpack-encore-bundle
- composer require symfony/ux-react
- npm run install --force
- npm install -D tailwindcss postcss autoprefixer postcss-loader
- npm install @babel/preset-react@^7.0.0 --save-dev
# config tailwind
- npx tailwindcss init -p
- Dans webpack.config.js à la fin du fichier : .enablePostCssLoader()
![webpackconfig-tailwind](image.png)
- Dans tailwind.config.js on dit a tailwind où trouver les fichiers a modifier : 
    ".assets/**/*.js",
    "./templates/**/*.html.twig",
![tailwind-config-js](image-1.png)
- Dans assets/styles/app.css on charge le tailwind pour que ça fonctionne: 
@tailwind base;
@tailwind components;
@tailwind utilities;
![tailwind-app-css](image-2.png)

# Vérification
- npm run build

# Lancer le serveur symfony
- symfony serve -d
- dans un onglet de navigateur : https://127.0.0.1:8000

# Installer Babel
- npm install @babel/preset-react@^7.0.0 --save-dev
- dans webpack.config.js decommenter .enableReactPreset()

# Suite installation React UX:
- dans assets/app.js ajouter ceci (si il y est pas déjà): // assets/app.js
import { registerReactControllerComponents } from '@symfony/ux-react';
registerReactControllerComponents(require.context('./react/controllers', true, /\\.(j|t)sx?$/));

# Controleur React : 
- ils sont créés dans assets/react/controllers
- c'est eux qui fourniront les codes React à utiliser dans twig

## Voir le résultat dans un navigateur :
- Lancer le server symfony : symfony server:start
- Lancer npmpour qu'il puisse lire le tailwind: npm run watch

## Utilisation dans Twig de React.js
- par exemple dans assets/react/controllers on a créé une props "{fullName}"
![prosp-fullName](image-3.png)
- pour l'utiliser dans un fichier twig : {{ react_component('NOM FICHIER CONTROLLEUR REACT', <div { 'NOM DE LA PROPS': 'VALEUR DE LA PROPS' }) }} ></div>

![utilisation-props-dans-twig](image-4.png)
