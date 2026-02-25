# Backstage K8S

Doc oficial: <https://backstage.io/docs/deployment/k8s>

## Create Namespace and Secret

```bash
kubectl create namespace backstage
kubectl create secret generic postgresql-secret \
  --from-literal=POSTGRES_PASSWORD=postgresspw \
  --from-literal=POSTGRES_USER=postgres \
  -n backstage  
```

## Create PVC

```bash
kubectl apply -f postgresql-pvc.yaml    
kubectl apply -f postgresql.yaml  
```

## Deploy Backstage

```bash
kubectl apply -f backstage.yaml
```

```bash
kubectl -n backstage port-forward svc/backstage 20001:20001
kubectl port-forward --namespace=backstage svc/backstage 80:80
```
