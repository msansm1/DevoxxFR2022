# Hands on Java 17

dev.java

inside.java


## Stop doing that !

peut poser problème pour le futur après java 17 (mis For Removal)
* ne plus appeler : new Integer ().. => pour tous les types Integer, Float, Double, .... quand Vlahallala arrivera
  * faire Integer.valueOf()
* finalize() : appelée depuis le thread du GC, mène à des race conditions, ou a des connexions qui reste ouvertes car le finalize n'est pas appelé dans un temps court
  * à supprimer
  * implémenter AutoCloseable + try-with-resources


## Records

github JosePaumard/2022_DevNexus-lab

on ne peut pas étendre un record, un record ne peut étendre autre chose, pas de champ d'instance

peut implémenter une interface, une méthode d'instance, champs ou méthodes statiques

un record est contient des composants (champs déclarés à la création du record)

on peut créer des annotations spécifiques aux composants des records

l'état d'un record est défini par ses composants

constructeur canonique => constructeur "de base" du record

réécrire un constructeur => copier une liste par exemple (copie défensive - avec List.copyOf()), permet de s'assurer l'immutabilité de la liste dans le record
* le faire aussi dans l'accessor pour être complet

pour de la validation, on peut utiliser un constructeur compact

la désérialisation d'un objet ne fait pas appel au construteur d'un objet


## Pattern matching

project amber (référence livre Amber - Zelazny)

```
if (o instanceof String name) {
    println(name);
}
```
Si o est une instance de String alors on créé la variable name.

Record pattern matching (preview java 19)
```
if (o instanceof User(String name, int age)) {
   name...;
}
```

Array pattern matching
```
if (o instanceof String[] {s1, s2}) {
   s1...;
}
```

Sur une liste
```
for (Point(int x, int y) : points)
```

Pour les switch
```
switch (shape) {
    case Square square -> square.edge()...;
    case Circle circle -> Math.PI*circle.radius()...;
    default -> 0;
}
```


## Sealed type

```
sealed interface Shape permits Square, Circle {}
```
Seules Squares et Circle peuvent implémenter Shape.

==> switch précédent : le default n'est plus nécessaire

si le switch n'est plus exhaustif le code ne compile plus (ex : ajout d'un type Rectangle).


## Guarded pattern

syntaxe à partir de la 19
```
case Square (int edge) when edge == 0 -> 0;
```


## Futur du pattern matching

déconstruction à partir du pattern Factory (si pas un record)

```
if (s instanceof String.format("test phrase %s and %d", String s, int d)) {
    // utilise s et d
}
```

il y aura normalement une syntaxe pouor créer des déconstructeurs dans les POJOs


