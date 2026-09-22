Google Cloud Platform est le troisième fournisseur de cloud public derrière AWS et Azure.
Il se distingue par trois chose :
- l'analytique de données (BigQuery)
- l'IA/ML (machine learning)
- Kubernetes (que google a crée)

GCP donne accès aux entreprises, aux **services et infrastructure de google**, comme les serveurs, la puissance de calcul, du stockage, du réseau...
Elle met pas les infrastructures directement, elle met des ressources informatique conçu pour fonctionner a grand echelle.

Le modèle est le paiement à l'usage (pay-as-you-go).
La facturation est automatique et a la seconde avec un minimum de 60 secondes.
Elle possède aussi des remises automatique quand une ressource tourne une grande partie du mois.


| Service GCP        | Rôle                                                                                                                                                                                                                         |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Compute Engine** | machines virtuelles à la demande                                                                                                                                                                                             |
| **Cloud Storage**  | stockage d'objets dans des _buckets_                                                                                                                                                                                         |
| **Cloud SQL**      | bases relationnelles managées ([MySQL](https://blog.stephane-robert.info/docs/services/bdd/relationnelles/mysql/), [PostgreSQL](https://blog.stephane-robert.info/docs/services/bdd/relationnelles/postgresql/), SQL Server) |
| **GKE**            | Kubernetes managé                                                                                                                                                                                                            |
| **BigQuery**       | entrepôt de données analytique _[serverless](https://blog.stephane-robert.info/docs/cloud/fondamentaux/serverless-faas/)_                                                                                                    |
| **Cloud Run**      | conteneurs _serverless_                                                                                                                                                                                                      |
| **VPC**            | réseau privé (global chez GCP)                                                                                                                                                                                               |
| **Vertex AI**      | plateforme IA/ML (modèles Gemini)                                                                                                                                                                                            |
En DB GCP propose aussi AlloyDb (PostGre haute perf) et Spanner, une base de données relationelle distribuée a l'echelle mondiale.

Trois domaines ou GCP est souvent cité en premier.

- La donnée avec BigQuery.
Un entrepôt de données serverless qui analyse des pétaoctets sans gérer de cluster.
On charge les données, on écrit du SQL, GCP gère le calcul et la mise à l'échelle.
Pour des équipes data, c'est fréquemment l'argument décisif.

- L'IA et le machine learning.
Google conçoit ses propres [TPU](https://fr.wikipedia.org/wiki/Tensor_Processing_Unit).

- Kubernetes a la source. Google a crée Kubernetes avant de le confier CNCF.
  GKE est donc le kubernetes managé de l'inventeur, avec un mode AutoPilot où google gère entierement les noeuds.
  
A linverse D'aws, le VPC(Cloud Privé) est une ressource générale qui n'a pas de limite géographique.

- AWS est leader dans la largeur du catalogue avec une grande maturité
- Azure est le cloud d'intégration microsoft (windows éclatax)
- GCP se différencie sur la data, l'ia, Kubernetes et un modèle tarifaire avantageux.
  
  