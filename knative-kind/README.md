# Set up a local Knative environment with KinD

These instructions follows this [tutorial](https://knative.dev/blog/articles/set-up-a-local-knative-environment-with-kind/)

### Install Kind 

[kind](https://github.com/kubernetes-sigs/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

Install Kind following the [site instructions](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).

### Create a cluster

Create a Kubernetes cluster using the clusterconfig.yaml file

````shell
kind create cluster --name knative --config clusterconfig.yaml
````
or run the following command: 

````shell
bash <(curl -s -L https://raw.githubusercontent.com/snowdrop/k8s-infra/main/kind/kind-reg-kourier-knative.sh)
````

This script creates a Kubernetes cluster using kind tool and deployes a a private docker registry and Kourier to route the traffic

## Install Knative environment with KinD
From [this tutorial](https://knative.dev/blog/articles/set-up-a-local-knative-environment-with-kind/)


### Install Knative Serving
````shell
kubectl apply --filename https://github.com/knative/serving/releases/download/knative-v1.0.0/serving-crds.yaml
````

````shell
kubectl apply --filename https://github.com/knative/serving/releases/download/knative-v1.0.0/serving-core.yaml
````

### Set up networking using Kourier
````shell
kubectl apply --filename kourier.yaml
````

Then, run the following commands:
````shell
kubectl patch configmap/config-network \
--namespace knative-serving \
--type merge \
--patch '{"data":{"ingress-class":"kourier.ingress.networking.knative.dev"}}'
````

````shell
kubectl patch configmap/config-domain \
--namespace knative-serving \
--type merge \
--patch '{"data":{"127.0.0.1.sslip.io":""}}'

`````

### Deploying your first app

````shell
kubectl apply --filename service.yaml
````

`````shell
kubectl get ksvc
`````
or 
````shell
kn service list
````

Request the service by running:
```shell
curl -v http://helloworld-go.default.127.0.0.1.sslip.io
```

#### Tips

Use kubectl ctx to change the context and install Knative, for example:
````shell
kubectx knative-kind
````

`kubectx` will show the available contexts.

##### Some used links:
