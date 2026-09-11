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


## Continuous Deployment : Sans humain

Un dev merge sa pull request, 5 minutes plus tard, le corde tourne en prod pour de vrais utilisateurs, **sans que personne n 'ai fait l'action de cliquer sur déployer**.

Cette étape du CI-CD mérite une exigence stricte a ce stade du projet.
La **couverture de test** doit être **excellente**.

#FeatureFlag
On doit pouvoir désactiver certains morceaux de code fraîchement déployé en cas de problème.
Les **features flags** (ou toggles) permettent de déployer du **code désactivé**.
Ca permet de **couper du code défectueux**, c'est un **interrupteur,** pas une machine a remonter dans le temps.

#RollbackAuto
Si les métriques de production dégradent après un déploiement, la pipeline doit revenir automatiquement à la version précédente.
Sans attendre d'intervention humaine.

#ObservabilitéAvancée
Détecter un problème rapidement.
Alerte sur les métriques clés, dashboard en temps réel, logs centralisés.
Voir le problème permet de le corriger.

#CultureBlameless
Avec des déploiements auto, les incidents peuvent arriver.
L'équipe doit traiter chaque incident comme une opportunité d'amélioration, pas comme une faute à punir. Sinon les devs auront peut de merge.

IMPORTANT : Les équipes qui pratiquent le CDeployment ont des années de dev sur le projet.
Des tonnes de test et une infra rodée.
Ce n'est pas un point de départ, c'est une destination.

![[Pasted image 20260909095839.png]]


Dans l'ordre :
1. Commencer par le CI
	 C'est la priorité absolue. Personne ne devrait push du code sans validation automatisée.   
	Au minimum :
	   - Chaque PR/Commit déclenche une pipeline
	   - Les tests unitaires bloquent le merge si ils échouent
	   - Le feedback arrive en moins de 10 minutes.

2. Evoluer vers la Delivery
	Une fois la CI stabilisée, ajoutez :
	- La construction d'artefacts immutables (images docker, binaires versionnées)
	- Le déploiement automatisé en staging après chaque merge
	- Des tests end-to-end sur l'environnement de staging
	- Une validation humaine avamt le déploiement en production
	Pour la plupart des projet, ce niveau de maturité est suffisant. La validation humaine reste centrale et est souvent la bonne réponse.

3. Considérer le Deployment
	Cette étape nécessite un réel questionnement
	- Avons-nous une couverture de test suffisante
	- Pouvons-nous détecter un problème de prod en moins de 5 minutes ?
	- Avons nous des mécanismes de rollback automatique ?

Le mieux est de rester en CDelivery jusqu'au moment ou la validation humaine n'a plus aucune valeur.
C'est a ce moment qu'on peut considérer un CDeployment.

##### BREF :
- CI : Valider chaque commit automatiquement.
- Delivery : Code toujours déployable, déploiement sur décision humaine. Recommandé.
- Delpoyment : Délpoiement automatique en prod.
  Exige une haute maturité.
- Chaque niveau inclut le précédent. Pas de raccourci.