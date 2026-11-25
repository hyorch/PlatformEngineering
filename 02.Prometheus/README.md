# Monitor with Kube-Prometheus-Stack

Install Helm
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
chmod 700 get_helm.sh
./get_helm.sh
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

Download Helm Chart
```bash
helm pull oci://ghcr.io/prometheus-community/charts/kube-prometheus-stack
```

```bash
helm upgrade --install kube-prometheus-stack .
```