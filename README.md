# tetragon-lab

## Build a one-node Kubernetes Cluster

Automate the cluster creation process

```
curl https://raw.githubusercontent.com/n1g3ld0uglas/AutomateK8/main/master.sh | bash
```

Automate the install of a CNI plugin (Calico):

```
curl https://raw.githubusercontent.com/n1g3ld0uglas/AutomateK8/main/install-calico.sh | bash
```

## Install tetragon

If you do not have helm, install it via the below command <br/>
NB: You might need admin priviliges - run ```sudo su```

```
snap install helm --classic
```

```
helm repo add cilium https://helm.cilium.io
helm repo update
helm install tetragon cilium/tetragon -n kube-system
kubectl rollout status -n kube-system ds/tetragon -w
```

## Deploy a Demo App

```
kubectl create -f https://raw.githubusercontent.com/cilium/cilium/v1.11/examples/minikube/http-sw-app.yaml
```

### Raw JSON events
The first way is to observe the raw json output from the stdout container log:
```
kubectl logs -n kube-system ds/tetragon -c export-stdout -f
```

To print out the logs on all tetragon pods, you will need to use a filter/selector such as ```-l app.kubernetes.io/name=tetragon```:
```
kubectl logs -n kube-system -l app.kubernetes.io/name=tetragon -c export-stdout -f
```

# Install tetragon-cli

```
dpkg --print-architecture
```

OUTPUT: amd64

```
curl -L --remote-name-all https://github.com/cilium/tetragon/releases/download/tetragon-cli/tetragon-linux-amd64.tar.gz{,.sha256sum}
```

Valid Packages: <br/>
https://github.com/cilium/tetragon/releases/tag/tetragon-cli

```
sha256sum --check tetragon-linux-amd64.tar.gz.sha256sum
```

OUTPUT: <b>OK</b>

```
sudo tar -C /usr/local/bin -xzvf tetragon-linux-amd64.tar.gz
```

OUTPUT: <b>tetragon</b>

```
rm tetragon-linux-amd64.tar.gz{,.sha256sum}
```

To start printing events run:
```
kubectl logs -n kube-system ds/tetragon -c export-stdout -f | tetragon observe
```
