
| Terme           | Explication simple                                                                                                                  |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Cluster         | Un groupe de machines (physiques ou virtuelles) qui travaillent ensemble pour faire tourner vos applications                        |
| Node            | Une machine dans le cluster. Peut être un "server" ou un "agent"                                                                    |
| Server<br>(K3s) | La machine qui prend les décisions : où lancer les applications, comment les exposer au réseau, etc.<br>C'est le cerveau du cluster |
| Agent<br>(K3s)  | Une machine qui exécute les applications. Elle reçoit ses ordres du server. C'est la "force de travail"                             |
| Control plane   | L'ensemble des composants qui gèrent le cluster (API, scheduler, etc).<br>Sur K3s, c'est le role du "server"                        |
| Pod             | La plus petite unité dans kubernetes : un ou plusieurs conteneurs qui tournent ensemble                                             |
| kubeconfig      | Un fichier qui contient les informations de connexion à votre cluster (adresse, certificats, tokens)                                |
| Token           | Un mot de passe secret qui permet aux agents de rejoindre le cluster                                                                |
Pour lister les services :
```bash 
kubectl get svc
```

Pour lister les Pods (conteneurs)
```bash
kubectl get pods
```

Editer le fichier de config d'un déploiement
```bash
kubectl edit deployment <nom_du_déploiement>
```

Voir les logs du déploiement
```bash
kubectl logs deployment/<nom_du_déploiement>
```

Pour lister les images du cluster
```bash
k3s ctr images ls
```

Plus simple
```bash
k3s crictl images
```

Pour exposer les ports d'un certain déploiement :
```bash
kubectl expose deployment <nom_du_déploiement> --port=80 --target-port=8080 --type=NodePort
```
 Pour supprimer des élément
 ```bash
 kubectl delete svc/deployment <nom_de_l'élément>
 ```

Explication d'un deploiement kubernetes dans un fichier de config
```bash
kubectl explain deployment
```
 