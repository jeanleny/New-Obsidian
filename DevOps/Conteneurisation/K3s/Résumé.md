Kubernetes est un orchestrateur.
Il gère plusieurs déploiement d'applications et les relient entre elles.

C'est comme un docker compose mais avec plein de fonctionnalités en plus.

Il peut remplacer dynamiquement des containers qui plantent pour éviter l'arrêt du service par exemple.

Un docker compose tourne sur une seule machine, k3s se divise en plein de petite machine.
K3s est utilisé pour un déploiement a grande échelle et en continu, tandis que compose va faire un travail plus local sur un seul hôte.

Le Cluster :
C'est tout  le système, toutes les machines qui tournent entre elles avec l'API de kubernetes celle avec qui on communique.

Le Control Plane (server node), c'est le cerveau.
Ca fait tourner l'API de k3s. Il décide qui fait quoi.

Les agents, ce sont les travailleurs.
Le Control plane leurs dit quoi faire, ils exécutent (pull images, starts containers via containerd).

Ils utilisent des Pods, qui est la plus petite unité de kubernetes. Ce sont des conteneur.

Toute l'instance k3s est configuré par le [[Config.yaml k3s]]

Le registries.yaml k3s lui explique comment containerd doit se comporter.
Quelles images avec quelles credentials...

