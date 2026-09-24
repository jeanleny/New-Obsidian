On peut construire une image d'application basique et l'importer dans K3s.
Cela permet de la déployer dans le cluster.

```bash
docker build -t <tag_name_wanted:version> <path/to/dockerfile>
```

then save it and redirects it to k3s instance:
```bash
docker save <tag_name:version> | sudo k3s ctr images import -
```
