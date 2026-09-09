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

###### Jobs vs Steps
Un **job** s'exécute sur une machine virtuelle dédiée. Plusieurs jobs peuvent tourner en parallèle sur des machines différentes.

Les **steps** d'un même job s'exécutent séquentiellement sur la même machine. Ils partagent le même système de fichiers.

