La market place est la place du marché des actions de workflow github actions
Ces actions sont communautaires donc nécéssite beaucoup de contrôle.
Actions est l'owner officiel de Github Actions et possèdent la plupart des actions.
Il y a aussi les owners possèdant le badge Verified Creator.

Plusieurs reflexe de sécurité concernant les actions du marketplace:
###### Utilliser le sha du commit d'une action plutot que le tag qui est mutable
```yaml
# ❌ Tag mutable - peut changer sans prévenir
- uses: actions/checkout@v4

# ✅ SHA immuable - vous contrôlez exactement le code exécuté
- uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
```

pour le récuperer via lapi de git : 
```bash
curl -s https://api.github.com/repos/actions/checkout/commits/v4 | jq -r .sha
gh api repos/actions/checkout/commits/v4 --jq .sha
```

###### Vérifier avec OpenSSF Scorecard

[OpenSSF Scorecard](https://scorecard.dev/) analyse la maturité sécurité d'un projet open source. Entrez l'URL du repository de l'action pour voir son score.

Un score élevé indique que le projet suit les bonnes pratiques : branch protection, signed releases, dependency updates, etc.

#### Paramètre d'action
La plupart des actions acceptent des paramètres via la propriété `with`:
```yaml
- uses: actions/setup-python@5fda3b95a4ea91299a34e894583c3862153e4b97 # v7.0.0
  with:
    python-version: '3.12'      # Version de Python
    cache: 'pip'                # Activer le cache pip
    cache-dependency-path: |    # Fichiers pour le cache
      requirements.txt
      requirements-dev.txt
```

Les actions possèdent souvent des documentation détaillées pour connaître les paramètres disponible.

##### Créer sa propre action

Si on crée un fichier yaml contenant notre action :
`.github/actions/setup-project/action.yml`

Qui va configurer notre projet :
```yaml
name: 'Setup Project'
description: 'Configure l''environnement du projet'

runs:
  using: 'composite'
  steps:
    - name: Setup Node.js
      uses: actions/setup-node@820762786026740c76f36085b0efc47a31fe5020 # v7.0.0
      with:
        node-version: '20'
        cache: 'npm'

    - name: Install dependencies
      shell: bash
      run: npm ci

    - name: Verify installation
      shell: bash
      run: npm --version && node --version
```
Et on l'appelle dans notre workflow :
```yaml
steps:
  - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1
  - uses: ./.github/actions/setup-project  # Action locale
```
