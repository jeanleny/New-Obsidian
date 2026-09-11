
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
