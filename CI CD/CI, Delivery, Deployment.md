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

A chaque CI :
A chaque commit ou pull request, la pipeline exécute automatiquement:
- Compilation
- Tests Unitaires
- Tests d'intégration (Les composants fonctionnent t-ils ensemblent ?)
- Analyse statique (conventions, lintage, formatage)
- Scan de sécurité
