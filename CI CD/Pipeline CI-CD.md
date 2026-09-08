Avant, pour d2ployer un programme, on utilisait des scrips bash.
Ca exécute sur notre machine, ça ne garde aucune trace, il faut le lancer manuellement et si ça foire on n'a aucune infos.

Une **Pipeline** c'est un **système d'exécution gouverné**.

- Ca s'exécute sur un serveur dédié/environnement contrôlé.
- Ca efféctue un retour détaillé des évenement lors des différentes étapes (linter, units test...)
- Historique complet de qui, quand, quoi...
- Tout cela est déclenché **automatiquement** comme un système d'usinage bien ficellé (push, pull request, tag...)
![[Pasted image 20260908112255.png]]

Le **Job** est une tâche exécutée dans la pipeline.
On peut avoir un Job de Build, de Test unitaire, de Docker, de Déploiement sur serveur ou kubernetes, de Sécurité...
- lint : Verifie le style du code
- unit-test : execute les tests unitaire
- build-docker : Construit une image Docker
- deploy-staging : Deploie sur l'environnement de test.
C'est la plus petite unité d'exécution, il faut l'imaginer comme un petit conteneur jetable qui fait son travail avant de disparaître.
Ils sont tous dans un **environnement isolé** et produisent un résultat binaire : Succès ou échec
On appelle ce résultat un **Artefact**
C'est le produit d'un job, le livrable d'une étape.

Le **Stage** est un ensemble de job avec le même objectif.
Ils **s'exécutent dans l'ordre**, mais les jobs d'un même stage peuvent tourner en **parallèle.**
