Voici un exemple de workflow pour une api Python
```YAML
name: CI Pipeline

# Permissions minimales déclarées au niveau du workflow
permissions:
  contents: read

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-24.04
    steps:
      # Actions épinglées par SHA
      - uses: actions/checkout@b4ffde65f46336ab88eb53be808477a3936bae11 # v4.1.1

      - name: Installer Python
        uses: actions/setup-python@0b93645e9fea7318ecaed2b359559ac225c90a2b # v5.3.0
        with:
          python-version: '3.12'

      - name: Installer les dépendances
        run: pip install -r requirements.txt

      - name: Lancer les tests
        run: pytest
```

Ce workflow :
- Déclare `permissions: contents : read` pour limiter les accès
- Utilise des SHA au lieu de tags pour les actions
- Fait exactement ce qu'il doit faire : tester le code

**Runs on** : La machine virtuelle utilisée pour exécuter le workflow.
IMPORTANT : Toujours mettre un tag de version fixe pour éviter les mauvaises surprise en cas d'update d'un `latest`

###### Le nom
```yaml
name: Tests unitaires
```
C'est le nom qui apparaît dans l'interface Github, dans l'onglet "Actions".
Il est important de bien choisir son nom pour s'y retrouver quand on en a plusieurs.

###### Le declencheur (trigger)
```yaml
on:
  push:
    branches: [main]
```
Le déclencheur définit quand le workflow s'éxecute.

###### Les jobs
```yaml
jobs:
  test:
    runs-on: ubuntu-24.04
    steps:
      - run: npm test
```
Les jobs definissent ce que fait le workflow.
Un job est un **ensemble de tâches (steps)** qui s'éxecutent sur une même machine.

Un job est une unité de travail **indépendante**.
Chaque job :
- S'exécute sur sa propre machine virtuelle (appelée **runner**)
- Peut contenir plusieurs étapes (**steps**)
- Peut contenir d'autre jobs ou s'exécuter en parallèle

***Executer des jobs dans un ordre précis*** (**needs**)

A la manière du depends on de docker compose, un workflow peut s'exécuter dans un ordre précis avec le mot clé needs qui définit quels jobs a besoin d'être terminé avant de se lancer.
```yaml
jobs:
  build:
    runs-on: ubuntu-24.04
    steps:
      - run: echo "Build"

  test:
    runs-on: ubuntu-24.04
    needs: build            # Attend que "build" soit terminé
    steps:
      - run: echo "Test"

  deploy:
    runs-on: ubuntu-24.04
    needs: [build, test]    # Attend que les deux soient terminés
    steps:
      - run: echo "Deploy"
```

Utiliser une action (uses)

```yaml
steps:
  - name: Récupérer le code
    uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1  # v7.0.1

  - name: Configurer Node.js
    uses: actions/setup-node@820762786026740c76f36085b0efc47a31fe5020  # v7.0.0
    with:
      node-version: 20
```

Une **action** est un bloc de code réutilisable. Plutôt que de réécrire la logique pour "récupérer le code du repo" ou "installer Node.js", vous utilisez une action existante.