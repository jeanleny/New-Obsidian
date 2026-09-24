Ce fichier sert a copnfigurer le processus k3s en lui-même.

Il sert a comment le serveur/agent k3s se lance and comment ses composants sont configurés.
Il ne va pas toucher aux pods k3s ou aux images.

Cela va surtout toucher aux paramètre globaux au réseau au cloud...
Voila un exemple de serveur très simple :

```yaml
# Kubeconfig lisible sans sudo
write-kubeconfig-mode: "0644"

# Désactiver les composants non nécessaires
disable:
  - traefik
  - servicelb
```
