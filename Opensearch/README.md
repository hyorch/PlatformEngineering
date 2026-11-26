# Opensearch K8s Helm Install

https://docs.opensearch.org/latest/install-and-configure/install-dashboards/helm/

## Opensearch
```bash
helm repo add opensearch https://opensearch-project.github.io/helm-charts/
helm repo update
helm pull opensearch/opensearch
tar xvzf opensearch*.tgz
cd opensearch
# Edit values.yaml file to set custom parameters
helm -n opensearch upgrade --install opensearch .
```

## Opensearch-Dashboards
```bash
helm repo add opensearch https://opensearch-project.github.io/helm-charts/
helm repo update
helm pull opensearch/opensearch-dashboards
tar xvzf opensearch-dashboards*.tgz
cd opensearch-dashboards
# Edit values.yaml file to set custom parameters
helm -n opensearch upgrade --install opensearch-dashboards .
```