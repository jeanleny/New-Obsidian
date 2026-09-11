K3s est une distribution Kubernetes légère (~70MB) qui intègre dans un seul binaire tous les composants nécessaires : 
- Containerd
- Flannel
- CoreDns
- Metrics-server

Conçu pour les environnements edge, IoT et les homelabs, K3s démarre en quelques secondes avec des ressources minimales.

Quand choisir K3s :
- Déploiement sur serveur Physique ou vms
- Haute disponibilité native
- Ressources limitées
- Cluster persistant

K3s permet de garder un aspect compact du logiciel avec tout les éléments de base disponible.

Un seul binaire `/usr/local/bin/k3s` est téléchargé
Ce binaire contient Kbernetes + tous les outils annexes
Un service systemd démarre et gère le tout
![[Pasted image 20260911145157.png]]

Composant intégrés a K3s :

| Composant      | Ca sert a quoi                                                         |
| -------------- | ---------------------------------------------------------------------- |
| Containerd     | Fait tourner les conteneurs (comme Docker mais en plus light)          |
| Flannel        | Crée le réseau virtuel pour que les pods communiquent entre eux        |
| CoreDNS        | Permet aux pods de se trouver par nom au lieu de passer par l'ip       |
| kube-proxy     | route le trafic réseau vers les bons pods                              |
| metrics-server | Collecte les stats CPU/RAM pour kubectl top                            |
| Traefik        | Ingress controller : expose vos apps sur le réseau externe             |
| ServiceLB      | simule un load balancer cloud pour les services de type `LoadBalancer` |
| local-path     | Crée des volumes persistants sur le disque local                       |

Mode de datastore :
K3s supporte plusieurs backends pour stocker l'état du cluster

|Mode|Quand l'utiliser|Description|
|---|---|---|
|**SQLite (kine)**|Mono-serveur (défaut)|Simple, fiable, fichier local. Parfait pour apprendre ou un homelab léger|
|**Embedded etcd**|HA (3+ serveurs)|Activé avec `--cluster-init`. Réplication + quorum entre serveurs|
|**Datastore externe**|Infra existante|MySQL, PostgreSQL ou etcd externe. Utile si vous avez déjà une DB managée|

###### Ressources minimales 
Un server consomme davantage dès qu'il héberge des pods applicatifs en plus du control plane, et sur un cluster à trois serveurs l'etcd intégré ajoutes sa propre empreinte mémoire tout en réclamant un disque rapide.