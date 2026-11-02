# ArgoCD

https://argo-cd.readthedocs.io/en/stable/getting_started/

```bash
kubectl create namespace argocd
kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

ArgoCD Cli

```bash
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

Access no Ingress

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Initial Password

```bash
kubectl -n argocd get secrets argocd-initial-admin-secret -o yaml
echo "xxxdfjlskdfñ" | base64 -d
```
