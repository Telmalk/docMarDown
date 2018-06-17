# Bem

* block
* Element `__`
* modifier `--`


```html
<ul class="hederNav headerNav--xmas">
  <li class="headerNav__item">
    <a class="herderrNav__itemLink headerNav__itemLink--active">
      A propos
    </a>
  <li class="headerNav__item">
    <a class="herderrNav__itemLink headerNav__itemLink--isDisable">
      Acceuil
    </a>
  </li>
```

```scss
.headerNav {
  &--xmas {
    background: red;
  }
  &__item {
    list-style: none;
  }
  &--itemLink {
    text-decoration: none;
    &--isDisabled {
      color: grey
    }
    &--isActive {
      color: green;
    }
  }
}

```


# Pseudo attribut ::after && ::before

Les pseudos attributes `before` et `after` sont essentiellement utilisé pour ajouter des éléments à votre DOM pour décorer sans que cela ait un impact sur le référencement ou botre HTML. IMPORTANT il est obligatoir d'avoir un `content: ''` afin que vos after / before s'affichent. Vous pouvez leur donner une taille, une position (absolute par rapport a son parent) essentiellement utilisé pour de la décoration.


```html
  <section class="cover">
    <h2 class="cover__title">Présentation</h2>
  </section>
```

```css
.cover {
  &__title {
    font-size: 24px;
    color: #bbb;
    text-align: center;
    position: relative;
    &::before,
    &::after{
      content: '';
      position: absolute;
      top: 0;
      display: block;
      width: 50px;
      height: 50px;
      background: green;
    }
    $::before {
      left: 0;
    }
    $::after {
      right: 0;
    }
  }
}
```

## Unité

### REM

L'unité de mesure REM est basée sur la taille du HTML ("élement racine du HTMML"). Par défaut, la taille du <html> est de 16px, ce qui veut dire que `1rem` = 16px. Pour évité de deviur faure des calculs afin de respecter les tailles relatives à votre maquette, vous pouvez ré-écrire cette `font-size` afin que `1rem = 10px`.


Equal to the computed value



```CSS
  html {
    /*
    override de la valeur par défaut
    afin que 1rem = 10px
    */
    font-size: 65.5%;
  }

  .mainTitle {
    font-size: 2.4rem;
  }
  .cover {
    width: 32rem;
  }
```


### EM

Le EM contrairement



```sass

html {
  font-size: 100%
}

.cover {
  height: 100px;
  $-tittle {
    font-size: .8em;
  }
  $-subTittle {
    font-size: .6em;
  }
}
```

## Les grilles avec flexboxgrid

[documentation](https://www.flexboxgrid.com)
[exemple](https://github.com/Telmalk/FlexboxGrid.git)


## Info balise css

box-sizing permet de mettre des padding a une div sans en changer la taille;
directio: rtl permet de changer la direction du texte -> rlt = rigth to the left;

# Liste Outils de veilles / Personne à suivre

## Tools

   * Pocket 
   * Medium
   * Timepage
   * Ulysse / iA writter
   * Feedly / Netvibes
   * uplabs
   * hreftools
   * placeholder
   * Scoop.it

## Medium https://medium.com/

   * Axel Calandre
   * dark… ariel dorol
   * Sacha Greif
   * FrontEnd Daily
   * Addy Osmani
   * Christian Heilmann
   * Aymeric Galissot
   * Chrome Developers
   * Sashing Magazine
   * Inside Designmodo
   * Polymer
   * Codecademy
   * inVision
   * Philip Sporrer
   * Matthew Thorry
   * Code school
   * Alex Devero
   * Joe David
   * Codeburst
   * ITNext
   * Hacker noon
   * Freecodecamp
   * Tiffany W. Eaton
    
## Twitter www.twitter.com


   * @Jason Miller
   * @VuejsNews
   * @nuxt_js
   * @Sean Thomas Larkin
   * @Vuejs Feed
   * @Even You
   * @Vuejs
   * @kentcdodds
   * @stolinski
   * @dan_abramov
   * @wesbos
   * @thecodinglove
   * @reactjs
   * @CodyWebHouse
   * @eggheadio
   * @MengTo
   * @addyosmani
   * @Real_CSS_Tricks
   * @timberners_lee
   * @Codecademy
   * @smashingmag
   * @digitalocean
   * @scaleway
   * @lukew

### Info Sécrurité


   * @malwrhunterteam
   * @troyhunt
   * @fs0c131y
   * @fossbytes
   * @UnaPibaGeek
   * @Damien_Bancal
   * @x0rz


### Backend

   * @fabpot
   * @dunglas
   * @mholt6

### Trouver un job


   * Welcolme to the jungle
   * Indeed
   * Remixjobs
   * hellowork.io
   * angel.co
   * chooseyourboss.com

### Freelance stuff


   * Awesome tools for Freelance
   * Shine Banque en ligne pour les AE
   * Invoice Ninja Gerer les factures / devis etc
   * Malt Offres Freelance
   * Comet Offres Freelance


#Es6

## Declaration fonction es6

* La fonction fléché  ne possédde pas ses propres valeur pour this, arguements, super, new.target. Ca permet d'éviter de bind sa fonction

````ecmascript 6

const maFonction = (arguement) => {
}
````

### L'objet arguments

* L'objet arguments est un objet, semblable à un tableau, correspondant aux arguments passés à une fonction.
````javascript

function maFonction(a, b, c) {
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2]);

}

maFonction(1, 32, 54);
````

## Ajax

* Exemple code Ajax avec xhr

````javascript

var search = document.querySelector('.search');
var input = search.querySelector('input');
var results = search.querySelector('.results');

var ajax = function(method, url, fn) {
  var xhr = new XMLHttpRequest();
  xhr.addEventListener('load', function() {
    if (xhr.readyState === 4) {
      fn(JSON.parse(xhr.response));
    }
  });
  xhr.open(method, url);
  xhr.send();
}

input.addEventListener('keypress', function(event) {
  if(event.keyCode !== 13 || !input.value) {
    return
  }

  ajax('GET', 'https://api.github.com/search/repositories?access_token={token}&q=' + input.value, function(data) {
    results.innerHTML = '';
    results.classList.toggle('visible', data.items.length > 0);

    for (var i = 0; i < Math.min(data.items.length, 3); i++) {
      results.innerHTML += '<span class="result">' + data.items[i].full_name + '</span>';
    }
  });
});

````

* Exemple de code Ajax avec fetch

````javascript

var search = document.querySelector('.search');
var input = search.querySelector('input');
var results = search.querySelector('.results');

input.addEventListener('keypress', function(event) {
  if(event.keyCode !== 13 || !input.value) {
    return
  }

  fetch('https://api.github.com/search/repositories?access_token={token}&q=' + input.value)
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    results.innerHTML = '';
    results.classList.toggle('visible', data.items.length > 0);
    for (var i = 0; i < Math.min(data.items.length, 3); i++) {
      results.innerHTML += '<span class="result">' + data.items[i].full_name + '</span>';
    }
  });
});
````

## Templating ES6

* exemple de Templating avec ES6

````ecmascript 6

const template = (args) => {
    let myTemplate = `
        <div>
            <p>${args[0]}</p>
            <p>${args[1]}</p>
            <p>${args[2]}</p>
            <p>Score: ${args[3]}/3</p>
        </div>
    `;
    return myTemplate;
};

document.body.innerHTML = template("Wehsh", "Bien ?", "Ou Bien ?", 2);
````
## Templating ES6

* exemple de Templating avec ES6

````ecmascript 6

const template = (args) => {
    let myTemplate = `
        <div>
            <p>${args[0]}</p>
            <p>${args[1]}</p>
            <p>${args[2]}</p>
            <p>Score: ${args[3]}/3</p>
        </div>
    `;
    return myTemplate;
};

document.body.innerHTML = template("Wehsh", "Bien ?", "Ou Bien ?", 2);
````

# TypeScript

* TypeScript permet un typage statique optionnel des variables et des fonctions, la création de classes et d'interfaces, l'import de modules, tout en conservant l'approche non-contraignante de JavaScript. Il supporte la spécification ECMAScript 6.

* Exemple de Typages en TypeScript

````typescript

let maValeurBooleenne: boolean = false;
let maChaineDeCaractere: string = "Hello World";
let monNombre: number = 1;
function maFonction(): string {
    return "Ma valeur de retour";
}
````

* Les class en TypeScript

````typescript

class MaClass {
    private _firstname;
    private _lastname;

    public constructor(firstname: string, lastname: string) {
        this._firstname = firstname;
        this._lastname = lastname;
    }

    public direBonjour(): string {
        return "Bonjour " + this._firstname + ", " + this._lastname;
    }
}

let monObjet = new MaClass("titi", "toto");
monObjet.direBonjour();
````

# Canvas

* Quelques Lien pour le canvas

* https://jsfiddle.net/j2n0ptmf/
* https://www.html5canvastutorials.com/
* https://www.sitepoint.com/html5-canvas-tutorial-introduction/
* https://internethistory.yahoo.co.jp/2017/

# WebPack

* article intéressant pour bien débuter avec WebPack https://www.alsacreations.com/tuto/lire/1754-debuter-avec-webpack.html
