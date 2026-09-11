Github Actions est la **plateforme d'automatisation** CI/CD intégrée nativement à GitHub.

Tout repose sur des **workflows** : des fichiers **YAML** placés dans le dossier `.github/workflows/` du repo.
Chaque workflow définit : 
- **Quand** s'exécuter (push, pull request, schedule)
- **Quoi** faire (Une série de jobs et steps)
- **Où** le faire (sur des machines virtuelles appelées runners)
```YAML

# Exemple minimal d'un workflow
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-24.04
    steps:
      - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1  # v7.0.1
      - run: npm test
```

**A chaque push, git détecte automatiquement les workflows du dossier.**
En fonction il :
- provisionne une VM
- Un runner exécute les tâches
- Un résultat est produit (succès/echec, artefacts, déploiement)

![[Pasted image 20260909141301.png]]

La grande force de Github Actions est le **MarketPlace**.
Des milliers d'Actions prêtes a l'emploi crées par la communauté et les éditeurs.
Plutôt que de réecrire la logique pour "déployer sur AWS" ou "envoyer une notification Slack", des addons existe déja.

Github Actions est **GRATUIT** pour les projets OpenSource
![[Pasted image 20260909140256.png]]

Sécurité IMPORTANTE :

Les attaques sur les pipelines CI/CD ont explosé. En mars 2025, une action GitHub compromise (`tj-actions/changed-files`) a permis d'exfiltrer les secrets de **milliers de dépôts en quelques heures**. L'attaque a touché toutes les versions de v1 à v45, y compris celles considérées comme "stables".

Les tags Mutables :
Dans les workflows github actions on va écrire des actions avec des tags Git : 
`uses: actions/checkout@v4`

Voici ce qui peut se passer :

1. Vous utilisez `actions/checkout@v4` dans votre workflow
2. L'action fonctionne parfaitement pendant des mois
3. Un attaquant compromet le compte du mainteneur
4. Il modifie le tag `v4` pour pointer vers du code malveillant
5. **Votre prochain pipeline exécute le code de l'attaquant**, sans que vous changiez quoi que ce soit

La solution : épingler par SHA
Le SHA (Secure Hash Algorithm) est l'empreinte cryptographique d'un commit.
Contrairement à un tag, il est immuable, impossible de le modifier sans changer le hash.
![[Pasted image 20260909144112.png]]
