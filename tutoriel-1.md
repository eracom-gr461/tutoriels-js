# Tutoriel 1: Génération d'aléatoire

Choses à connaître:
- Insérer du code JavaScript dans une page
- Définir une variable
- Définir une fonction
- Sélectionner un élément avec "getElementById"
- Modifier un élément avec "style"

Dans ce tutoriel (basé sur le projet de Julien Nshimirimana), nous allons afficher l'heure, les minutes et les secondes sous forme de chiffres.
La position des chiffres varie, respectivement toutes les secondes, minutes et heures.

Nous commençons par créer la structure HTML qui servira à l'affichage:

```html
<time class="temps" id="heure">00:00:00</time>

<time class="temps" id="minute">00:00:00</time>

<time class="temps" id="seconde">00:00:00</time>
```

Nous décidons d'utiliser l'élément HTML `<time>`, créé pour afficher des informations de temps ou date.

Nous donnons un identifiant à chaque élément (heure, minute, seconde). Cet "id" servira à les modifier avec du JavaScript.

Nous voulons à présent faire deux choses qui nécessiteront du JavaScript: 

1) Afficher l'écoulement des heures / minutes / secondes.
2) Positionner de manière alétoire les éléments.

Commençons par la première étape: l'affichage de l'heure.

## Afficher l'heure

Pour afficher l'heure, nous allons devoir "produire" l'heure courante, puis la "transporter" dans l'élément HTML approprié. 

Une fois l'heure courante définie, nous stockerons les minutes, secondes et heures dans des "variables", qui seront régulièrement renouvelées.

Il faut pour cela comprendre ce qu'est une **variable**. Une variable est un mot-clé auquel on assigne une valeur (chiffre, texte, ensemble de données), afin de la réutiliser facilement. On utilise ce type de procédé en mathématiques (a+b=c), ou en comptabilité (revenu brut - charges salariales = revenu net). Les charges salariales sont une variable, qui sera définie p.ex. à 7.66%.

Pour "produire" la date courante, nous utilisons une méthode "prête à l'emploi" inclue dans JavaScript. C'est la méthode "Date", qui permet de produire un affichage de date et d'heure, dans divers formats.

Voici comment fonctionne cette méthode:

```javascript
var date = new Date;
```

- Le premier mot, **"var"**, indique que nous allons définir une **variable**. 
- Le deuxième mot, **"date"**, est le nom que nous avons décidé de donner à la variable. Nous aurions pu choisir n'importe quel mot, p.ex. "pizza", "chouFleur" ou "delta9". On doit se limiter à des lettres et des chiffres (pas d'espaces, accents ou signes de ponctuation). Dans le cas de mots composés ("chou-fleur"), la convention en JavaScript est d'utiliser des majuscules (comme dans "chouFleur").
- Le signe "=" précède la définition de la variable.
- "new Date" est la méthode JavaScript à laquelle nous faisons appel, qui produit un "objet date", contenant toutes les informations : année, mois, jour, heure, minute, seconde, milliseconde...

Cet "objet-date" est maintenant stocké dans la variable "date", mais il est invisible. Si on décide de l'afficher, on peut écrire la ligne JavaScript suivante:

```javascript
console.log(date);
`` 

Ce qui produira l'affichage suivant dans la console JavaScript de notre navigateur: 

```
Thu Sep 21 2017 20:51:51 GMT+0200 (CEST)
```

Il s'agit de la date / heure telle qu'elle est réglée sur votre ordinateur (si elle est fausse, c'est que l'horloge de votre appareil est déréglée).

Ces informations sont trop détaillées, pour nos besoins. Nous allons donc extraire les **heures**, **minutes** et **secondes**. Là aussi, le JavaScript propose des fonctions prêtes à l'emploi: `getHours()`, `getMinutes()` et `getSeconds()`.

Voici par exemple comment obtenir les secondes, à partir de notre variable "date":

```javascript
var seconde = date.getSeconds();
``` 

- On connait déjà le **"var"**, c'est le mot annonçant qu'on définit une variable.
- **"seconde"** est le nom que nous décidons de donner à notre variable. On serait aussi libre d'écrire "Sec", "zknd", ou "s"... L'idéal est d'utiliser des noms de variables facilement compréhensibles, pas trop longs.
- Après le "=", on utilise la variable "date", à la suite de laquelle on colle la fonction "getSeconds()". Le fait de les séparer avec un point est important: ce caractère créé un enchaînement, la partie de gauche étant l'origine, sur laquelle agit la partie de droite.

Le fait que "getSeconds()" se termine par une paire de parenthèses nous indique qu'il s'agit d'une "fonction".  Une fonction, en JavaScript, c'est un ensemble d’instructions prêt à être utilisé. Dans certains cas, on peut insérer un contenu entre les parenthèses, p.ex. une variable qui sera modifée par la fonction. Ici ce n'est pas le cas, cette fonction étant très simple: elle va simplement retourner les secondes à partir d'un objet "Date". 

Une fois cette ligne de code exécutée, nous disposons donc d'une variable "seconde", qui contient un chiffre entre 0 et 59, donné par l'horloge de votre ordinateur.

Si nous voulons définir heure/minute/seconde, nous pouvons procéder de cette manière:

```javascript
var date = new Date;
var minute = date.getMinutes();
var seconde = date.getSeconds();
var heure = date.getHours();
```

Nous avons défini nos variables, voyons maintenant comment les afficher. 

C'est l'occasion de découvrir une opération très puissante du JavaScript : la modification des contenus d'une page web.

Pour modifier le contenu, nous devons effectuer deux actions: 

- **Sélectionner** l'objet HTML qui servira de conteneur.
- Effectuer la **modification** du contenu.


