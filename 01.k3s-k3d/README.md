# K3S and K3D Kubernetes

k3s is a lightweight Kubernetes distribution. k3d is a tool that runs k3s clusters inside Docker containers. They’re complementary, not alternatives: k3d uses k3s under the hood.

## K3S

### Install

```bash
curl -sfL https://get.k3s.io | sh -
sudo cp /etc/rancher/k3s/k3s.yaml  .kube/config
```

### Uninstall

```bash
/usr/local/bin/k3s-uninstall.sh
```

### Redirect port

```bash
kubectl -n <namespace> port-forward svc/<service> <local-port>:<service-port>

kubectl -n istio-system port-forward svc/kiali 20001:20001
```

## K3D - k3s in Docker

Deploy a k3d cluster ready to Istio deployment. https://istio.io/latest/docs/setup/platform-setup/k3d/

```bash
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

k3d cluster create --api-port 6550 -p '9080:80@loadbalancer' -p '9443:443@loadbalancer' --agents 2 --k3s-arg '--disable=traefik@server:*'


k3d cluster list
kubectl cluster-info
kubectl config get-contexts
kubectl config use-context k3d-k3s-default
```

Start and stop the cluster.

```bash
k3d cluster stop --all
k3d cluster start --all
```

## kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

source /usr/share/bash-completion/bash_completion
echo 'source <(kubectl completion bash)' >>~/.bashrc
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
```
