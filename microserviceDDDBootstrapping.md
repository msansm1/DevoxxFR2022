## Microservices, DDD et bootstrapping pour un microservices

structures des microservices :

application -> domaine (entités + aggrégats) -> infrastructure

couche transverse DTO : application & domaine

## Création d'un nouveau µservice

projet µservice -> un domaine

hérite d'un framework maison (quelques trucs de base, config, ...)

plein de modules -> génération de code ?

Telosys :
* templates
* config projet
* model

pour le templating -> s'appuie sur apache velocity

bundle de templates -> un bundle ~ une couche fontionnelle / technique

tout en fichiers textes

quasiment tout est personnalisable via les templates

modèle extensible via tags

choix de MyBatis car modèle trop compliqué, clés composite, JPA gère mal et SpringDataJDBC pas du tout

génération requêtes SQL, modèle liquibase

génération DTO + Factory

contrôleurs avec API complète et annotations, et appels aux services

génération des TU, TI, batchs, bootstrapping de l'IHM (crud)


## Gains

productivité

simplification

standardisation

qualité


## Jusqu'où aller ?

équilibre temps création templates / temps de développement gagné

privilégier les quick-wins


## Quel générateur de code

simple & léger

prise en main rapide

OSS

jetable (pas de lock-in)

indépendant de l'IDE

adaptable & flexible

