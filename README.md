# Set up a local Kubernetes environment with KinD

### Install Kind

[kind](https://github.com/kubernetes-sigs/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

Install Kind following the [site instructions](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).

### Create a cluster

Create a Kubernetes cluster and set up an Ingress controller, either follows the instructions from [here](https://kind.sigs.k8s.io/docs/user/ingress/#create-cluster) or run the following command:

````shell
bash <(curl -s -L https://raw.githubusercontent.com/snowdrop/k8s-infra/main/kind/kind-reg-ingress.sh)
````

This script creates a Kubernetes cluster using kind tool and deploys a private docker registry and NGINX controller to route the traffic

If you want to set up a Knative environnement jump to the [knative-kind instructions](./knative-kind/README.md).