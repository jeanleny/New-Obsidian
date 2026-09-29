
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
Ces images contiennent la paquet manager apk et la suite [[Busybox]].