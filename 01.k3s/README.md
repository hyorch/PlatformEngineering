# K3S Kubernetes

## Install

```bash
curl -sfL https://get.k3s.io | sh -
```

## Uninstall

```bash
/usr/local/bin/k3s-uninstall.sh
```

## Redirect port

```bash
kubectl -n <namespace> port-forward svc/<service> <local-port>:<service-port>

kubectl -n istio-system port-forward svc/kiali 20001:20001
```
