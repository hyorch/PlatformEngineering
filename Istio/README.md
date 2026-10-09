# Istio

Istio deployment using cli.

## Istio Download Cli

```bash
curl -L https://istio.io/downloadIstio | sh -
```

Add to *.bashrc* istio-x.y.z/bin path.

```txt
# istio
PATH=/home/jpastor/istio-1.31.1/bin:$PATH
```

```bash
istioctl version
```

## Deploy Istio Operator

```bash
istioctl install --set profile=demo
```
