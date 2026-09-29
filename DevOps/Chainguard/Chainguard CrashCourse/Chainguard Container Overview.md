
Les containers chainguard sont sécurisés, renforcés et crée pour avoir le moins de CVE possible.

### Wolfi Linux distro minimaliste
Wolfi est une distribution crée par chainguard pour tourner sur des containers.
Elle n'a été conçue que dans ce but.
Architecture minimale pour composer nos images sans bloat.
Wolfi utilise l'APK (Alpine Package Keeper) pour la gestion des paquets, ce qui facillite les [[Reproducible builds]].
Les packages sont définis dans des fichiers YAML qui permettent une sophistication des pipelines d'automatisation.

En réduisant la taille de l'OS, la surface d'attaque devient bien mien vulnérable mais prennent aussi beaucoup moins de place.

Attestation de provenance et [[SBOM]]