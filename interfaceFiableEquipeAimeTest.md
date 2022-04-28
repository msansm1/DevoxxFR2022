## Make your interfaces reliable by making your team love testing !

pour du front

## Comment tester

100% de couverture -> facile mais pas forcement un indicateur fiable

!! tests trop techniques

tester les features !

tester un flow complet à l'écran => on s'en fout de l'implem, simplification du refacto

test avec "gherkin"

génération livingdoc à partir des tests

si on teste tous les chemins -> détection code mort

mock uniquement dépendances externes


## Comment faire un test

un bug -> un test

TDD appliqué au bugfix

tests les plus petits possibles

avec le legacy -> on teste uniquement la nouvelle fonctionnalité, bien se limiter à ça


## Réalisation

snapshotDiff

https://github.com/johnmeunier/talk-test

librairies
- msw -> service worker de mock d'API pour tests front
- testing library
- specflow


## Limitations TDD

que pour les devs à l'aise avec l'environnement technique

pas avec snapshot :)


https://docs.google.com/presentation/d/1ysnu8QNdpg1pc-FqFqOg1oeg6jPsHKXgpe9sFtTMbTU/edit#slide=id.gab0243390c_0_33
