# Tutoriel 1: Génération d'aléatoire

Choses à connaître:
- Insérer du code JavaScript dans une page
- Définir une variable
- Définir une fonction
- Sélectionner un élément avec "getElementById"
- Modifier un élément avec "style"

Dans ce tutoriel (basé [sur le projet de Julien Nshimirimana](https://github.com/eracom-gr461/jsclocks-juliusboy)), nous allons afficher l'heure, les minutes et les secondes sous forme de chiffres.

La position des chiffres varie, respectivement toutes les secondes, minutes et heures.

## Structure HTML

Nous commençons par créer la structure HTML qui servira à l'affichage:

```html
<time id="heure">00</time>
<time id="minute">00</time>
<time id="seconde">00</time>
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

### La fabrication du temps

Pour "produire" la date courante, nous utilisons une technique "prête à l'emploi" inclue dans JavaScript. C'est **[l'objet "Date"](https://www.w3schools.com/jsref/jsref_obj_date.asp)**, qui permet de produire un affichage de date et d'heure, dans divers formats.

Voici comment faire appel à cet objet:

```javascript
var date = new Date;
```

Explication:
- Le premier mot, **"var"**, indique que nous allons définir une **variable**. 
- Le deuxième mot, **"date"**, est le nom que nous avons décidé de donner à la variable. Nous aurions pu choisir n'importe quel mot, p.ex. "pizza", "chouFleur" ou "delta9". On doit se limiter à des lettres et des chiffres (pas d'espaces, accents ou signes de ponctuation). Dans le cas de mots composés ("chou-fleur"), la convention en JavaScript est d'utiliser des majuscules (comme dans "chouFleur").
- Le signe **"="** précède la définition de la variable.
- **"new Date"** est la technique permettant de créer un "objet date", contenant toutes les informations : année, mois, jour, heure, minute, seconde, milliseconde...

Cet "objet-date" est maintenant stocké dans la variable "date", mais il est invisible. Si on décide de l'afficher, on peut écrire la ligne JavaScript suivante:

```javascript
console.log(date);
```

Ce qui produira l'affichage suivant dans la console JavaScript de notre navigateur: 

```
Thu Sep 21 2017 20:51:51 GMT+0200 (CEST)
```

Il s'agit de la date / heure telle qu'elle est réglée sur votre ordinateur (si elle est fausse, c'est que l'horloge de votre appareil est déréglée).

### Définissons nos variables

Ces informations sont trop détaillées, pour nos besoins. Nous allons donc extraire les **heures**, **minutes** et **secondes**. Là aussi, le JavaScript propose des fonctions prêtes à l'emploi: `getHours()`, `getMinutes()` et `getSeconds()`.

Voici par exemple comment obtenir les secondes, à partir de notre variable "date":

```javascript
var seconde = date.getSeconds();
``` 

Explication:
- On connait déjà le **"var"**, c'est l'instruction annonçant qu'on définit une **variable**.
- **"seconde"** est le nom que nous décidons de donner à notre variable. On serait aussi libre d'écrire "Sec", "zknd", ou "s"... L'idéal est d'utiliser des noms de variables facilement compréhensibles, pas trop longs.
- Après le **"="**, on utilise la variable **"date"**, à la suite de laquelle on colle la méthode **"getSeconds()"**. Le fait de les séparer avec un point est important: ce caractère créé un enchaînement, la partie de gauche étant l'origine, sur laquelle agit la partie de droite.

Le fait que "getSeconds()" se termine par une paire de parenthèses nous indique qu'il s'agit d'une **fonction**.  Une fonction, en JavaScript, c'est un ensemble d’instructions prêt à être (ré)utilisé. Dans certains cas, on peut insérer un contenu entre les parenthèses, p.ex. une variable qui sera modifée par la fonction. Ici ce n'est pas le cas, cette fonction étant très simple: elle va simplement retourner les secondes à partir d'un objet "Date". 

Une fois cette ligne de code exécutée, nous disposons d'une variable "seconde", qui contient un chiffre entre 0 et 59, donné par l'horloge de votre ordinateur.

Si nous voulons définir heure/minute/seconde, nous pouvons procéder de cette manière:

```javascript
var date = new Date;
var minute = date.getMinutes();
var seconde = date.getSeconds();
var heure = date.getHours();
```

### Modification des contenus

Nous avons défini nos variables, voyons maintenant comment les afficher. 

C'est l'occasion de découvrir une opération très puissante du JavaScript : **la modification des contenus d'une page web**.

Pour modifier le contenu, nous devons effectuer deux actions: 

- **Sélectionner** l'objet HTML qui servira de conteneur.
- Effectuer la **modification** du contenu.

Pour sélectionner l'objet, il fait décider par quel critère nous allons l'isoler: élément HTML, "id" ou "class". Souvenons-nous que notre HTML se présente comme ceci: 

```html
<time id="heure">00</time>
<time id="minute">00</time>
<time id="seconde">00</time>
```

Il paraît logique d'utiliser le paramètre "id" pour sélectionner l'élément-cible. Ça tombe bien, JavaScript propose la méthode [getElementByID](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById), qui sert précisément à cela!

Voici un exemple d'utilisation: 

```javascript
document.getElementById('seconde');
```

Dans cet exemple, nous sélectionnons un élément HTML possédant l'identifiant 'seconde'. Cela correspond dans notre cas à l'élément `<time id="seconde">00</time>`.

Comment modifier le contenu de cet élément? Là aussi, une méthode JavaScript existe: `[innerHTML](https://developer.mozilla.org/fr/docs/Web/API/Element/innertHTML)`.

Voici comment remplacer le contenu de notre élément `<time>` avec `innerHTML`:

```javascript
document.getElementById("seconde").innerHTML = "texte qui va remplacer le contenu";
```

Puisque nous souhaitons mettre à la place du contenu le numéro enregistré dans la variable "seconde", voici un meilleur exemple:

```javascript
document.getElementById("seconde").innerHTML = seconde;
```

**Important:** Dans cette ligne de code, le mot `seconde` après le signe "=" s'écrit **sans guillemets**, car c'est une **variable**. Si nous avions laissé des guillemets, ce serait le mot "seconde" en toutes lettres qui s'afficherait. En JavaScript, ce qui est entouré de guillemets est du texte, pas du code. En l'absence de guillemets, les mots doivent correspondre à des méthodes JavaScript, ou des variables définies – sans quoi, nous aurons des erreurs.

### Une action répétitive

Nous savons maintenant comment afficher un chiffre dans un élément de notre page ... mais comment effectuer cette action à répétition, une fois par seconde?

Nous utiliserons la méthode JavaScript prévue pour ce besoin, `setInterval()`. Voici comment cette méthode fonctionne:

```javascript
var monIntervalle = setInterval(function() {
	  metronome();
  }, 1000); 
```

Explications:
- "var monIntervalle" définit une variable, monIntervalle étant le nom donné à notre intervalle. Cela n'a pas de conséquence, mais il est nécessaire de lui donner un nom pour le faire exister.
-  "setInterval" est la méthode que nous utilisons, suivie de "function()", qui nous permet de déclencher une fonction qui se répétera à intervalles réguliers. Nous devons donner un nom à cette fonction, nous avons choisi "metronome()". Il ne faudra pas oublier de la définir.
- "1000" est la durée de l'intervalle, définie en millisecondes. Avec la valeur de 1000, cela donne une seconde. 

---

## Démonstration

Pour voir le code de ce tutoriel exemple en action, [visitez cette page](tutoriel-1-code) et affichez [le code source](https://github.com/eracom-gr461/tutoriels-js/blob/master/tutoriel-1-code/index.html).