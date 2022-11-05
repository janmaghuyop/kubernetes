Kubernetes
==========
Kubernetes playground.

Links:
- https://github.com/k3s-io/k3s
- https://github.com/k3d-io/k3d
- https://github.com/kubernetes-sigs/kind
- https://github.com/k0sproject/k0s
- https://github.com/lima-vm/lima

Using lima k3s:
```bash
# start
cd tmp
limactl start template://k3s
limactl shell k3s sudo cat /etc/rancher/k3s/k3s.yaml > kubeconfig.yaml

export KUBECONFIG=$(pwd)/kubeconfig.yaml
kubectl get pods -A

# stop
limactl list
limactl stop k3s
```

Using lima k3d:
```bash
limactl start template://docker

# install k3d and create demo cluster
# https://github.com/k3d-io/k3d/releases
limactl shell docker curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | TAG=v5.4.6 bash
limactl shell docker k3d cluster create demo

limactl shell docker k3d kubeconfig get demo > kubeconfig.yaml
export KUBECONFIG=$(pwd)/kubeconfig.yaml
kubectl get pods -A

# stop
limactl shell docker k3d cluster stop demo
limactl stop docker
```
