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
Exemple de stage classique
- *Validate* : job lint et job tests en parallèle
- *Build* : Construction de l'artefact
- *Déploy* : Déploiement progressif
![[Pasted image 20260908131148.png]]

Découper en stage permet de trouver **rapidement** un problème et de ne pas effectuer tout le processus de construction du projet.
Ex : Si le linter fail -> la construction s'arrête.
Cela permet aussi une meilleur **lisibilité**, et une **optimisation de la construction** du projet de par la **parallélisation maximale** des différents jobs.

Voici un graph d'exécution en parallèle.
Ces graphes sont appellés **graphe acyclique dirigé** (DAG) *Directed acyclic graph*.
C'est un graphe a sens unique, c'est pour ça qu'il est acyclique.
![[Pasted image 20260908132052.png]]

Cela permet de visualiser les jobs sans rapport entre eux pour tourner en parallèle.

# Runners et Agents
###### Qui exécute le code ?

Un **runner** (Github actions, Gitlab Ci) ou **agent** (Jenkins, Azure DevOps) est la **machine** qui exécute vos jobs.
Les termes diffèrent fonction des plateformes utilisés.

Le flux d'exécution :
1. La plateforme de CI/CD assigne un job au runner/agent dispo
2. Le runner récupère le job (code, configuration)
3. Le job est exécuté par le runner
4. Le runner renvoie les logs et le statut à la plateforme

###### *type de runners*
Il y a les runners *hébergés* : (Github, Gitlab, Saas)
Les runners *auto-hébergé* : en local
Et les *éphémères* qui permettent une isolation maximale pour un temps plus long.

Ces différents types peuvent avoir des aspects changeant comme **la sécurité, la performance, le coût**.

Un **job** a accès a tout ce que le **runner** peut voir :
- **Système de fichier** du runner
- Les **variables d'environnement**.
- Le **réseau** accessible depuis le runner
Cela siginifie que si plusieurs projet partagent le mêne runner, certains **jobs malveillant** peuvent potentiellement **accéder aux donées** d'un autre projet.
C'est pourquoi on utilise les runners **éphèmères** pour des contextes plus sensibles.

###### Le **Cache** 
Il **conserve** des fichiers entre les exécutions pour éviter de les recalculer.

Le cache est caractérisé par plusieurs choses :
- Clé basée sur un **hash** (lockfile, branche)
- Il est optionnel, le job doit fonctionner même sans cache
- Partagé entre jobs et pipelines.

###### L'artefact
Ne sert qu'a transmettre des résultas, c'est le **produit d'un job**.
L'artefact est caractérisé par plusieurs choses :
- Attachés à un job précis
- Téléchargeables après la pipeline
- **Obligatoires** pour les jobs dépendant

###### Environnements de déploiement 
Un environnement représente une **cible** de déploiement.
La *dev, la staging, la prod,* tout ça sont des sortes d'étapes dans le développement.
