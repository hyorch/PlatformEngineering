# Monitor with Grafana Cloud

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
chmod 700 get_helm.sh
./get_helm.sh
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```


```bash
helm upgrade --install grafana-cloud \
  --namespace monitoring --create-namespace \
  grafana/k8s-monitoring \
  --set "cluster.name=k3d-jorge" \
  --set "collectorCommon.alloy.remoteConfig.enabled=true" \
  --set-string "collectorCommon.alloy.remoteConfig.url=https://fleet-management-prod-011.grafana.net" \
  --set-string "collectorCommon.alloy.remoteConfig.auth.username=******" \
  --set-string "collectorCommon.alloy.remoteConfig.auth.password=****************************" \
  --values - <<'EOF'
collectors:
  alloy:
    presets: [large, root, host-network, host-storage, host-cgroup, clustered, service-discovery, filesystem-log-reader, daemonset, otel-receiver]
    extraService:
      enabled: true
      name: otel-receiver

# Add these if Kubernetes monitoring is enabled
telemetryServices:
  node-exporter:
    deploy: true

  kube-state-metrics:
    deploy: true

  beyla:
    deploy: true
    k8sCache:
      replicas: 1

  opencost:
    deploy: false

  sdkInjector:
    deploy: true
    allowedConfigMapWriters: system:serviceaccount:monitoring:grafana-cloud-alloy
EOF
```
