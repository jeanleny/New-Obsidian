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


