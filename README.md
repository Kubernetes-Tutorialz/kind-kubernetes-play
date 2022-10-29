# Kind Kubernetes Play

In this short repository you can learn and simulate a Kubernetes environment in your local machine.

## What is Kind?
[kind](https://kind.sigs.k8s.io/) is a tool for running local Kubernetes clusters using Docker container “nodes”. kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

## Installation
You can install kind with `go get sigs.k8s.io/kind`. This will put `kind` in `$(go env GOPATH)/bin`. You may need to add that directory to your `$PATH` as shown here if you encounter the error `kind: command not found` after installation.

On Linux Systems:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

If you are using other operational system, please make sure you have check this [website](https://kind.sigs.k8s.io/docs/user/quick-start).

## Usage
To use kind, you will also need to install [docker](https://github.com/amaurybsouza/devops-cheatsheet/blob/main/docker-cheatsheet.md). Please, go ahead and install Docker before go to Kind.

- Once you have docker running you can create a cluster with:

`kind create cluster`

You will see the follow output:

```bash
# kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂
```

- To delete your cluster use:

`kind delete cluster`

## Creatinga cluster (Multi Node)
In this steps you going to create a Kind cluster with more nodes.

- Please make sure you have the follow `YML` code:

```yml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker
```
- Using the configuration above, run the following command.  It's will gives you a k8s v1.17.2 cluster with 1 control-plane node and 3 worker nodes.

`kind create cluster --config kind-config.yaml`

- Check if the cluster is working fine:

```bash
# kubectl get nodes
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   24h   v1.25.3
kind-worker          Ready    <none>          24h   v1.25.3
kind-worker2         Ready    <none>          24h   v1.25.3
kind-worker3         Ready    <none>          24h   v1.25.3
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)