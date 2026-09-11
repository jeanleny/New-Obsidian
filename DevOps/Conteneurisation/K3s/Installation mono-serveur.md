L'installation la plus simple : un serveur unique qui fait tourner le control plane et les workloads.

###### C'est quoi un cluster mono-serveur ?
Un cluster avec une seule machine qui fait tout : elle prend les décisions (control plane) ET exécute vos applications (workloads). 
C'est parfait pour :
- Apprendre Kubernetes
- Un homelab
- Des environnements de développement
- Des projets avec peu de trafic

Limitation : Si la machine tombe en panne, tout le cluster tombe.

1. **Installer K3s avec le script officiel**
```bash
curl -sfL https://get.k3s.io -o k3s-install.sh
less k3s-install.sh
sh k3s-install.sh
```

`curl -sfL https://get.k3s.io -o k3s-install.sh`
: télécharge le script d'installation dans un fichier
- `-s` : mode silencieux 
- `f` : échoue proprement si le serveur renvoie une erreur
- `-L` : suit les redirections
- `-o k3s-install.sh` : enregistre le script au lieu de le piper dans sh

- `less k3s-install.sh`: inspecte le script avant de l'exécuter
- `sh k3s-install.sh` : exécute le script une fois relu

**Ce que fait le script :**
1. Détecte votre OS et architecture (amd64, arm64...)
2. Télécharge le binaire K3s (~70 MB)
3. L'installe dans `/usr/local/bin/k3s`
4. Crée un service systemd `k3s.service`
5. Génère les certificats et le kubeconfig
6. Démarre K3s automatiquement

Vérfier l'install : `sudo systemctl status k3s`

Lister 
`sudo k3s kubectl get nodes`

Comment lire la sortie :

- **NAME** : le nom de la machine (hostname)
- **STATUS** : `Ready` = la machine fonctionne, `NotReady` = problème
- **ROLES** : `control-plane` = c'est un server K3s
- **AGE** : depuis combien de temps le node est dans le cluster
- **VERSION** : version de Kubernetes

Configurer kubectl pour notre utilisateur
Par défaut, le kubeconfig est lisible uniquement par root.
Pour utiliser kubectl sans sudo :
```bash
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
kubectl get nodes
```


###### Les fichiers importants
Ces chemins n'existent que sur un server: un agent n'a ni kuubeconfig ni `node-token`, il ne conserve que sa configuration locale et ses conteneurs. 
Le config.yaml est le seul fichier de la liste que K3s ne crée pas, c'est a vous de le déposer avant l'installation.

