Toutes les pipelines ne ressemblent pas.
Les architectures dépendent de notre contexte.
La taille de l'équipe, l'organisation du code, la fréquence de déploiement.

###### Mono vs Poly repo
Le schéma oppose deux organisation de dépôt.
Ce qui distingue les deux est le déclenchement : 
Le monoRepo regroupe tout les projet d'une entreprise dans un seul Repo :
Les projets Web/Mobile/librairies partagées sont **commune au même repo**.
Le PolyRepo lui possède **un Repo par famille de projet.**

![[Pasted image 20260909103115.png]]

###### Trunk Based vs branches longues

**Trunk Based** : tout le monde travaille sur main.
Les features durent moins de 24h. **Exige des Feature flags** pour les fonctionnalités en cours.

**Branches longues** `dev` `release` `main` : Plus de contrôle, mais **risque de conflits** ("merge hell").

###### Build once, deploy many
Principal fondamental : l'artefact est construit **une seule fois**, puis promu d'environnement en environnement. **Jamais de rebuild** par cible.
Cette étape permet de gagner du temps sur la construction :
Au lieu de construire l'application une fois par environnment :
Source Code
   ├── Build → Dev
   ├── Build → Test
   ├── Build → Staging
   └── Build → Production

 On le construit une **seule fois pour chaque environnement** : 
Source Code
     ↓
   BUILD
     ↓
Artifact v1.4.2
     │
     ├── Deploy → Dev
     │
     ├── Deploy → Test
     │
     ├── Deploy → Staging
     │
     └── Deploy → Production
