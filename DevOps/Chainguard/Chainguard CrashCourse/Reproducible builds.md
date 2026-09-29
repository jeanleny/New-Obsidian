Ce sont des pratique de developpement logiciel permettant de garantir qu'un même code source, compilé dans le même environnement et avec les mêmes instructions va produire un fichier binaire identique octet par octet peu importe qui effecture la compilation ou à quel moment.

Cela permet a nimporte quel tiers de vérifier de manière indépendante que le logiciel exécuté correspond exactement au code source.

Cela permet de lutter contre les attaques de la chaîne d'approvisionnement.
Cela empêche que du code ne soit instroduit au moment de la chaine de production ou de la compilation.

##### Plusieurs pratique:
On peut figer l'environnement de build
Avec Docker on s'assure du bon OS et on vérouille les dépendance avec des versions stables.

Neutraliser les variables dynamiques dans le code. Ce sont souvent des variables propre a la machine, (l'heure, les chemins).
On met une heure fictive (celle du commit), des chemins relatifs plutôt que strict.

On peut build deux fois le projet et vérifier les différences entres-elles.