
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
