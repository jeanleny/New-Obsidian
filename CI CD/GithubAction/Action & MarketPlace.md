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

