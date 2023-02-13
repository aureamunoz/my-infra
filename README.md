# Set up a local Kubernetes environment with KinD

### Install Kind

[kind](https://github.com/kubernetes-sigs/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

Install Kind following the [site instructions](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).

### Create a cluster

Now, you can create a cluster. If you want to set up a Knative environment jump to the [knative-kind instructions](./knative-kind/README.md).
If you want just a regular kubernetes environment with an ingress controller to manage the traffic, jump to the [k8s-ingress-kind instructions](./k8s-ingress-kind/README.md).