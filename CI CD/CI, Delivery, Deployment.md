Ces trois termes sont constamment confondus, ils représentent pourtant des niveaux d'automatisation très différents.
![[Pasted image 20260908155915.png]]

**Continuous Integration** (CI): minimum vital.
Chaque push déclenche compilation, tests, analyse.
Le feedback arrive en minutes. Si ça casse on le sait immédiatement.

**Continuous Delivery**: Le code est toujours prêt à partir en prod mais c'est quand même un humain qui le déclenche.

**Continuous Deployment**: Chaque modification validée part automatiquement en production.
Zéro intervention humaine. Exige une couverture de tests excellente et des mécanismes de rollback solides en cas de crash.

CI valide le code, Delivery le rend déployable.
Déployment le met en production automatiquement.
Plus on automatise plus les éxigences de qualité augmentent.

![[Pasted image 20260908161035.png]]

Cela Permet de détecter des problèmes immédiatement.


## Continuous Integration (CI)
A chaque CI :
A chaque commit ou pull request, la pipeline exécute automatiquement:
- Compilation
- Tests Unitaires
- Tests d'intégration (Les composants fonctionnent t-ils ensemblent ?)
- Analyse statique (conventions, lintage, formatage)
- Scan de sécurité

Avec le temps, le temps de correction d'un bug se rallonge et peut-être corrigé en plusieurs heures voire jours.
Grace au CI, le contexte du dévellopeur est toujours frais et permet d'être rapidement corrigé.

Règle d'or de la CI :
- Chaque commit déclenche la CI
- Un echec bloque le merge
- Les tests sont rapides
- Le feedback est immédiat (mail, slack, discord)

## Continuous Delivery
C'est le prolongement de la CI.
Le code est validé mais aussi prêt à être déployé en production à tout moment. Avec la validation d'un humain.

Après la CI qui valide le code, la pipeline Delivery prend le relais :
- Construit un **artefact** immuable, une image Docker, un binaire, un package
- Déploie un **environnement** de test
- Exécute des **tests end-to-end** (Créations d'utilsateurs et suppression, parcours d'achat, d'inscriptions)
- Attend une **validation**

La validation humaine est très importante pour certains contexte.

Le contexte métier et les nouvelles fonctionnalités liée a l'entreprise et sa direction.
L'environnement régulé comme la santé, l'aéronautique qui nécessite une documentation et une approbation au yeux de la loi.

Une CDelivery en construction.

## Continuous Deployment : Sans humain

