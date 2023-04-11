# NodeJS
> Learning

Installer NodeJS => via snapcraft pour la derniere version ou directement via la distro linux :neckbeard:

Lorsque NodeJS est installé npm vient avec.

La premiere étape pour crée un projet faire un dossier puis dedans faire un npm init

## npm
> Le gestionnaire de paquets

Il permet surtout d'installer des modules ou des packets dans notre projets ou sur notre pc/server

npm install express --save pour sauvegarder express par exemple uniquement sur notre projet

npm install express --global ici par contre express sera installer sur notre machine

## express
> Framework

Express intégre toute la structure front dans notre projet en NodeJS (les routes entre autres)
```
var express = require('express');
app = express();
EJS
Engine de views
```
EJS va permettre de crée des views avec le language HTML avec le Javascript intégré de dedans app.set('view engine', 'ejs'); et surtout durant le pointage sur get faire un retour sur le dossier/sousDossier de la view res.render("section/tech");

## CommonJS
> Construction

Permet de structurer un appel de fonction de maniére simplifié

Exemple: mod_test.js
```
module.exports = function(){
    var msg = "Ce module contient une string"; 
    return msg;
}
```
app.js
```
var express = require('express');
var msg = require('./mod_test');
[...]

app.listen(3000, function(){
    console.log(msg());
});
```
### Creation Structure
#### Config
> server.js

var express = require('express');
var app = express();
app.set('view engine', 'ejs'); 

module.exports = app;

> Arboressance
```
├──app
|   ├──config
|   |   ├──server.js
|   ├──routes
|   |   ├──home.js
|   |   ├──news.js
|   |   ├──formNew.js
|   ├──views
|   |   ├──index.ejs
|   |   ├──bar.ejs
|   |   ├──.ejs
```
### Consign
`npm i consign`
> Autload de script

Consign permet de chargé automatiquement les appels de models, routes, schema. conifigs, controllers, object maps... sans avoir a faire de déclaration de variable en superflue :godmode: `var routeTest = require('./app/routes/home')(app); ==> consign().include('app/routes).into(app)`;

Sur server.js

const express = require('express');
var consign = require('consign');

var app = express();

// views
app.set('view engine', 'ejs');
app.set('views', './app/views');

// MVC => consign
consign()
    .include('app/routes')
    .then('config/dbConnection.js')
    .into(app);

module.exports = app;
Base de Données
Mongodb(mongoose) seedling
Bibliotheque qui créee une connection entre Mongodb et Javascript npm i mongoose -s

const express = require('express');
const mongoose = require('mongoose');

var app = express();

app.set('view engine', 'ejs');
app.set('views', './app/views');

mongoose.set("strictQuery", false);

// la conf est directement visible sur ton mongo atlas 
mongoose.connect('mongodb+srv://pseudo:motdepasse@cluster.mongodb.net/?retryWrites=true&w=majority');


const db = mongoose.connection;

db.on("error", console.error.bind(console, "connection error: "));

db.once("open", function () {
    console.log("Bien connecter a la base de donnée Mongo");
});

module.exports = app;
Models
