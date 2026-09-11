Les credentials ne doivent jamais apparaître dans les fichiers de configuration ou dans le code.

Ceci :
```yaml
# ❌ JAMAIS FAIRE ÇA : même "pour tester vite fait"
- run: docker login -u admin -p "MonMotDePasse123"
```
Est totallement interdit dans une CI.

Les mots de passe reste dans **l'historique de Git pour toujours.**
Des bots scannent GitHub **24h/24** et trouvent les secrets en quelques minutes.
Si quelq'un **fork** le repo, il peut trouver le mot de passe **visible**.

La solution : **Les secrets Github**
Un secret GitHubb, c'est une variable spéciale stockée dans un coffre fort chiffré.
Il faut le voir comme un **gestionnaire de mot de passe intégré a GitHub** conçu pour les workflows.
![[Pasted image 20260910151132.png]]

Ce qu'il se passe lorsqu'on utilise un secret dans Workflow
- Creation dans les Settings (Secrets and variables 
-> Actions)
- GitHub le chiffre et le stocke dans coffre-fort
- Le workflow demarre et demande le secret
- GitHub déchiffre et injecte la valeur dans la variable d'environnement.
- Le script l'utilise sans jamais voir la valeur en clair dans les logs
