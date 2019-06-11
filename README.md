# kubernetes-gpu
Install NVIDIA GPU Support on CoreOS based Kubernetes Cluster

# Prerequisits
* CoreOS based Kubernetes cluster with GPU nodes (e.g. AWS P2 instances)

# Installation

## Using helm

Install helm via

```shell
helm init --service-account tiller
```

Install the provided helm chart

```shell
helm install --name gpu-installer --namespace kube-system charts/nvidia-installer
```

## Static manifests

First install the nvidia driver via this daemonset

```shell
kubectl apply -f https://raw.githubusercontent.com/gardener/gpu-installer/master/manifests/k8s-nvidia-driver.yaml
```

Wait until the init container finishes on each node and install the device plugin

```shell
kubectl apply -f https://raw.githubusercontent.com/gardener/gpu-installer/master/manifests/k8s-nvidia-deviceplugin.yaml

```

# Acknowledgments & References
* Build and install NVIDIA driver on CoreOS: https://github.com/squat/modulus
* Nvidia Device Plugin: https://github.com/kubernetes/kubernetes/blob/master/cluster/addons/device-plugins/nvidia-gpu/daemonset.yaml
