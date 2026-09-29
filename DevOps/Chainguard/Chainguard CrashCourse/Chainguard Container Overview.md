
Les containers chainguard sont sécurisés, renforcés et crée pour avoir le moins de CVE possible.

### Wolfi Linux distro minimaliste
Wolfi est une distribution crée par chainguard pour tourner sur des containers.
Elle n'a été conçue que dans ce but.
Architecture minimale pour composer nos images sans bloat.
Wolfi utilise l'APK (Alpine Package Keeper) pour la gestion des paquets, ce qui facillite les [[Reproducible builds]].
Les packages sont définis dans des fichiers YAML qui permettent une sophistication des pipelines d'automatisation.

En réduisant la taille de l'OS, la surface d'attaque devient bien mien vulnérable mais prennent aussi beaucoup moins de place.

#### Attestation de provenance et [[SBOM]]
En plus des faibles vulnérabilités, les containers Chainguard ont des artefacts signés pour attester :
- Quelle dépendances vont être utilisées pour établir l'environnement et l'endroit ou le build se produit.
- La config utilisé par cette image incluant les dépendances, les variables d'environnement ainsi que les entry-points. C'est important car si les images arrivent sur notre machine et commencent a :
	- exécuter en tant que root
	- contenir énormément de paquets
	- lance des terminaux
	C'est important de le savoir pour accroître la sécurité du container.
- La [[SBOM]] pour l'image est fournie

Les artefacts de chainguard sont signés avec [[Cosign]] et les signatures sont disponibles avec les images.

#### Migrer vers Chainguard
Chainguard est distroless par défaut, ce qui fait qu'ils n'ont pas de shell ou de package manager par défaut.
Ce qui en fait de très légère images a manipuler.
Cependant, chainguard peut utiliser des images avec le suffixe **-dev**.

1. Apk package manager
Ces images contiennent la paquet manager [[apk]] et la suite [[Busybox]].
C'est pour cela qu'il faut changer chacune des commandes de gestions apt pour apk.
2. Entrypoint behaviour
Dans certains cas, les images chainguar due a la nature des images distroless, ne peuvent pas reproduire le comportement de certains entrypoint.
Toujours se réferer a la documentation des containers Chainguard.

#### Travailler en multi-stage 
Vu que les containers sont distroless par défaut, avoir une image -dev permet d'être utilisé pour débuguer et construire le projet.
La meilleur utilisation de chainguard est de combiner des images distroless avec des images -dev en [[Multi-Stage]] build.

Dans l'étape du build, on installe toutes les dépendances et les tâche qui necessites apk pour construire les artefacts.
Dans le final stage on va juste copier tous les artefacts dans les environnement distroless.

#### Comprendre les versions d'images
Il y a deux stratégies utilisées dans les projets open-source pour mettre a jour leurs projet.
- On update tout le projet avec la dernière version pour tout le monde. Cela fonctionne pour de petits projets et des projets qui n'introduise pas forcément des changement drastiques dans les releases.
- On garde de nombreuses versions du projet pour permettre plusieurs versions laissant du temps aux utilisateurs de migrer sur les nouvelles. Ce qui est utilisés par de bien plus gros projets.

Dans les deux cas il est important de garder a jour les images utilisés, c'est l'une des étapes les plus importantes en termes de stratégies pour la maintenance du logiciel.

