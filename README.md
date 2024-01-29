# TOS_Internationalization

Ce TOS a pour but d'expliquer comment mettre en place l'internationalization sur NUXT 3.

## Étape 1 : Installer le package

Pour pouvoir utiliser l'internationalization, il est nécessaire d'utiliser ce package :

``` 
npm install @nuxtjs/i18n --save-dev
```

## Étape 2 : Mise en place du package 

Ensuite, dans votre fichier nuxt.config.ts, il faut rajouter ceci : 

```
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: [
    "@nuxtjs/i18n"
  ],
})
```

## Étape 3 : Création des fichiers de configuration

Il faut ensuite créer des fichiers de configuration en fonction des langues que vous voulez configurer au sein de votre site internet.
Ces fichiers seront dans un dossier « locales » qui sera au même niveau que les autres dossiers du projet.
Ces fichiers ont pour but de définir une balise qui servira de repère dans notre site pour qu'il puisse savoir en fonction de la langue quel texte afficher.

Pour les différents exemples, nous utiliserons l'anglais et le français.

Contenu du fichier en.json :
```
{
    "research": "Search",
    "usermenu": "Open user menu",
    "settings": "Settings",
    "signout": "Sign out",
    "mainmenu": "Open main menu",
    "home": "Home",
    "about": "About",
    "playlistmanage": "Playlist Management",
    "pricing": "Pricing",
    "contact": "Contact",
    "catalogmanage": "Catalog Management",
    "usermanage": "Users Management",
    "pricemanage": "Amount of payment",
    "barmanage": "Bar Management",
    "addbar": "Add Bar",
    "filter":"Filter",
    "barname": "Bar Name",
    "showing": "Showing",
    "addplaylist": "Add playlist",
    "playlistname": "Playlist Name"
}
```

Contenu du fichier fr.json : 
```
{
    "research": "Rechercher",
    "usermenu": "Ouvrir le menu utilisateur",
    "settings": "Paramètres",
    "signout": "Déconnexion",
    "mainmenu": "Ouvrir le menu principal",
    "home": "Accueil",
    "about": "A propos",
    "playlistmanage": "Gestion des playlists",
    "pricing": "Gestion des prix",
    "contact": "Nous contacter",
    "catalogmanage": "Gestion du catalogue",
    "usermanage": "Gestion des utilisateurs",
    "pricemanage": "Gestion des prix",
    "barmanage": "Gestion des bars",
    "addbar": "Ajouter un bar",
    "filter":"Filtrer",
    "barname": "Nom du bar",
    "showing": "Montrer",
    "addplaylist": "Ajouter une playlist",
    "playlistname": "Nom de la Playlist"
}
```

Il faut ensuite ajouter un nouveau fichier dans les plugins. 
Ce fichier permet de savoir la liste des langues présentes sur le site et l'endroit où il peut localiser les fichiers de configurations. 
Il faut ajouter le fichier i18n.ts dans le dossier « plugins » avec comme contenu :
```
import { createI18n } from "vue-i18n"
import en from "../locales/en.json"
import fr from "../locales/fr.json"

export default defineNuxtPlugin(({ vueApp }) => {
  const i18n = createI18n({
    legacy: false,
    globalInjection: true,
    locale: "en",
    messages: {
      en, 
      fr, 
    }
  })

  vueApp.use(i18n)
})
```

## Étape 4 : Configuration de la langue de départ

Maintenant, il faut écrire le code pour lui dire sur quelle langue il doit se baser en démarrant.
Ici, nous allons nous baser sur la langue de base configuré sur l'ordinateur de l'utilisateur.
Pour faire cela, il suffit de rajouter après la partie modules dans le fichier nuxt.config.ts :
```
  build: { 
    transpile: ["vue-i18n"] 
  }, 
  vite: { 
    plugins: [ 
      VueI18nVitePlugin({ 
        include: [ 
          resolve(dirname(fileURLToPath(import.meta.url)), "./locales/*.json") 
        ] 
      }) 
    ] 
  } 
```
Avec ce code, il saura quelle langue afficher à l'utilisateur au démarrage.

## Étape 5 : Mise en place des balises au sein du code

Il faut ensuite mettre les balises au sein du code pour afficher les bons labels pour les textes

```
{{ $t('research') }}
```

## Étape 6 : Mise en place du sélecteur des langues

Pour finir, il reste à ajouter au sein du site un sélecteur pour permettre le choix de langue.

Pour ce faire il suffit de rajouter dans le code :
```
      <select id="locale-select" v-model="$i18n.locale">
        <option value="en">en</option>
        <option value="fr">fr</option>
      </select>
```


# Conclusion

Et voila, vous avez l'internationalization de mise en place au sein de votre site.
