
###### Les trois réflèxes de sécurité
Dès votre premier workflow, adoptez ces pratiques :

1. Epingler les actions par **SHA**
	Toujours utiliser le sha complet pas le **tag Git**
```YAML
# Toujours utiliser le SHA complet, pas le tag
- uses: actions/checkout@b4ffde65f46336ab88eb53be808477a3936bae11 # v4.1.1
```
2. Déclarer des permissions minimales
	Par défaut, un workflow a TROP de permissions
	Limiter explicitement au strict nécessaire
```YAML
permissions:
	content: read #lecture seule sur le code
```

3. Ne jamais afficher de secrets dans les logs
```YAML
# ❌ CATASTROPHE : le secret apparaît dans les logs
- run: echo "Token: ${{ secrets.API_TOKEN }}"

# ✅ Les secrets sont masqués automatiquement si utilisés correctement
- run: curl -H "Authorization: Bearer ${{ secrets.API_TOKEN }}" https://api.example.com
```


Les workflows github actions ont accès a nos secrets(credentials), peuvent modifier notre code et déployer en production du code malveillant sans qu'on s'en rende compte.

La pipeline :
- **A accès aux secrets** : Tokens d'API, mots de passe de bases de données, clés de déploiement cloud...
- **Peut publier des packages** : sur npm, PyPY, DockerHub, ou notre registre privé
- **Peut deployer en production** : modifier ce qui tourne sur nos serveurs
- **Exécute du code sur des machines** : Peut avori accès a des réseau interne
Un attaquant de la pipeline peut avoir accès a tout.

###### L'attaque Supply Chain
Une attaque supply chain ne nous cible pas directement. Elle cible quelque chose que l'on utilise.
![[Pasted image 20260910111946.png]]

Même sans faille dans notre code on peut avoir des failles ailleurs :
- Une **action du marketplace** est compromise
- Une **dépendance npm** contient du code **malveillant**
- une **image docker** de base a  été **modifiée**

Exemple :
![[Pasted image 20260910112149.png]]

###### Les 3 risques principaux de Github Actions :
1. Les Secrets exposés
	La bonne pratique pour stocker les secret dans github :
	Settings -> Secrets et référencer les avec ${{secrets.NOM}} Github masque automatiquement dans les logs.

```yaml
# ✅ Le secret est stocké dans GitHub, pas dans le code
# Personne ne peut le voir, même dans l'historique Git
- run: curl -H "Authorization: Bearer ${{ secrets.API_KEY }}"
```

2. Les actions tierces non vérifiées
	Une action github est un bout de code réutilisable que que quelqu'un a publié. 
	C'est très pratique mais risqué, le code exécuté a accès a tout le workflow du projet.
```yaml
# ⚠️ Questions à se poser :
# - Qui est "random-user" ? Une entreprise ? Un particulier ?
# - Que fait vraiment cette action ? Ai-je lu le code ?
# - Est-elle maintenue ? Dernière mise à jour il y a 3 ans ?
- uses: random-user/deploy-magic@v1
  with:
    token: ${{ secrets.DEPLOY_KEY }}  # On lui donne nos clés !
```
Le mieux est d'utiliser les actions de sources fiable (Github, grandes entreprises, projets populaires).

3. Le code des pulls request
	**Qu'est-ce qu'une pull request (PR) ?** Une PR, c'est une proposition de modification du code. Sur un projet open source, n'importe qui peut forker le repo (en faire une copie), modifier le code, puis proposer ses changements via une PR.

	**Pourquoi c'est un vecteur d'attaque ?** Par défaut, quand quelqu'un ouvre une PR, les workflows du repo s'exécutent pour tester le code proposé. Un attaquant peut donc :