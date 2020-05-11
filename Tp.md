Consigne:

- insérer 3 points sur paris et mettre dans une collection
- insérer 1 point aléeatoire dans paris et trouver le point le plus proche de ce point aléatoire
- faire une zone ou deux point son inclus et un point exclu
- en partent d'un point, Trouver les point dans un rayon de 5km

Démarer le server :

```js
Start mongoD
```

Lancer la commande :

```js
Mongo;
```

Lister les database :

```js
show dbs
```

Lister les tables :

```js
show tables
```

Afficher les stats de la base de donnée

```js
db.stats();
```

Creer la collection places :

```js
db.createCollection("places");
```

Ce mettre sur la collection places :

```js
use places
```

Insérer plusieurs positions :

```js
db.places.insertMany([
  {
    name: "La Tour Eiffel",
    location: {
      type: "Point",
      coordinates: [48.85823, 2.29454],
    },
  },
  {
    name: "Notre Dame",
    location: {
      type: "Point",
      coordinates: [48.85272, 2.35056],
    },
  },
  {
    name: "Les Catacombes de Paris",
    location: {
      type: "Point",
      coordinates: [48.83383, 2.33242],
    },
  },
]);
```

Lister les valeurs dans la collection places avec une meilleur lisibilité :

```js
db.places.find().pretty();
```

insérer un point :

```js
db.places.insertOne({
  name: "Les Pavillons de Bercy Musée des Arts Forains",
  location: {
    type: "Point",
    coordinates: [48.83279, 2.38884],
  },
});
```

créer un index :

```js
db.places.createIndex({ location: "2dsphere" });
```

voir toutes les index :

```js
db.places.getIndexes();
```

trouver le point le plus proche de ce point aléatoire:

```js
db.places
  .find({
    location: {
      $near: {
        $geometry: { type: "Point", coordinates: [48.83279, 2.38884] },
        $maxDistance: 5000,
        $minDistance: 20,
      },
    },
  })
  .pretty();
```
