# API GATEWAY ISTIO

https://istio.io/latest/es/docs/tasks/traffic-management/ingress/gateway-api/


## Install Istio objects
```bash
kubectl get crd gateways.gateway.networking.k8s.io &> /dev/null || \
  { kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.4.0" | kubectl apply -f -; }

istioctl install --set profile=minimal -y
```

## Install App httpbind
```bash
 kubectl -n httpbind apply -f https://raw.githubusercontent.com/istio/istio/release-1.29/samples/httpbin/httpbin.yaml
```

## Create Gateway
```bash
kubectl create namespace istio-ingress
kubectl apply -f - <<EOF
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: gateway
  namespace: istio-ingress
spec:
  gatewayClassName: istio
  listeners:
  - name: default
    hostname: "*.example.com"
    port: 80
    protocol: HTTP
    allowedRoutes:
      namespaces:
        from: All
EOF
```

## Create HTTPRoute
```bash
kubectl apply -f - <<EOF
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: http
  namespace: httpbind
spec:
  parentRefs:
  - name: gateway
    namespace: istio-ingress
  hostnames: ["httpbin.example.com"]
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /get
    backendRefs:
    - name: httpbin
      port: 8000
EOF
```

## Test
```bash
kubectl wait -n istio-ingress --for=condition=programmed gateways.gateway.networking.k8s.io gateway
export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io gateway -n istio-ingress -ojsonpath='{.status.addresses[0].value}')

curl -s -I -HHost:httpbin.example.com "http://$INGRESS_HOST/get" 
```
