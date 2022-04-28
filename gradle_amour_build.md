# Donnez de l'amour à votre build, il vous le rendra !

Louis Jacomet & Paul Merlin


## Outil

analyse gratuite de build gradle publiée en ligne

`gradle --scan`



## Gradle

wrapper : bootstrap -> gradle-initializr.cleverapps.io

gradle 7.5 -> changement ordre taches JAR et tests : le JAR sera fait avant les tests


## Fonctionnalités JVM

### Catalogues de version

centraliser la liste des dépendances

coordonnées et versions

pas de classifier, exclude, ...

séparation group:artifact et version

groupes de dépendances

*Démo :*

gradle/libs.versions.toml
```
[versions]
nomversion = "version"
// strictly, prefered

[librairies]
nomlib = "group:artifact:version'
nom2-lib1 = { module = "group:artifact", version.ref = "nomversion" }

[bundles]
nombundle = ["nomlib", "nomlib2"]

[plugins]
```

build.gradle.kts
```
implementation(libs.nomlib)
api(libs.nom2.lib1)
```

nom2-lib1 -> groupe nom2, librairie lib1

permet de grouper les librairies

peut se faire dans le settings.gradle.kts avec dependenceResolutionmanagement si les libs définissent bien un catalogue de version (micronaut le fait)

limitations

* pas pour un plugin de settings
* ni script d'installation


### Java toolchains


build.gradle.kts
```
java {
    toolchain {
        languageVersion.set(JavaLanguageVersion.(of(17)))  ==> java 17 pour toutes les tâches
    }
}


tasks..... {
    javaLauncher.set(javaToolchains.launcherFor {
        languageVersion.set(JavaLanguageVersion.of(11))
    })  ==> spécifique
}
```

gère les sdk SDKMAN!

maven toolchains

on peut spécifier dans le gradle.properties où gradle peut chercher les SDK installés

Provisioner Java JDK -> pas au point encore (dû au changement adoptOpenJDK -> adoptium)

Futur :
* plugins pour provisioning JDK
* version plus précise
* GraalVM
* early-access
* ...

7.5 -> support checkstyle

les plugins ne supportent pas forcement les toolchains


### Suites de tests

en preview dans 7.4

```
testing {
    suites {
        val integrationTest by registering(JvmTestSuite::class) {
            useJUintJupiter()
            dependencies {
                implementation(libs.spock)  ==> évite testImplementation
            }
            targets {
                all {
                    testTask.configure {
                        javaLauncher....
                    }
                }
            }
        }
        val test by getting(JvmTestSuite::class) {
            targets {
                all {
                    testTask.configure {

                    }
                }
            }
        }
    }
}
```

dans le futur 
* permettre l'exécution sur différentes versions de Java
* intégration avec couverture de code


### Test fixtures

séparation des fixtures / code de test -> publication et consommation des fixtures

build.gradle.kts
```
plugin {
    `java-test-fixtures`
}


dependencies {
    testFixturesImplementation("")
}
```

on peut l'utiliser dans les test suites ==> spécifier les fixtures spécifiques nécessaires pour la test suite

plugin maven pour publier gradle module metadata

gradle 7.4 -> aggregation de résultats jacoco ou tests


### Publication

plugin maven-publisher
```
val javaComp = components["java"] as AdhocComponentsWithVariants
javacomp.withVariantsFromConfiguration(configurations.testFixturesImApiElements.get()) {
    skip()
}  => ne pas publier les fixtures avec le composant java

publishing {
    publications {
        create<MavenPublication>("maven") {
            from(components["java"])
        }
        pom {
            description: "a library"
        } => ne doit contenir que de la documentation, pas de modification du pom sinon désynchro avec fichier gradle
    }
    repositories {
        maven {
            url = uri("repository")
        }
    }
}
```

créé un dossier repository => permet de voir ce qui est publié

pour maven central, plugin io.github.....



## Logique de build

## Structure de build

## Performance

gradle-profiler -> installable avec sdkman

mesure le build

synchro IDE (uniquement android studio actuellement)

profiler

benchmarks

org.gradle.priority=low => sur machine de dev pour ne pas bloquer a machine en cas de build

