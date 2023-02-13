### Create a cluster

Create a Kubernetes cluster using the clusterconfig.yaml file

````shell
kind create cluster --config clusterconfig.yaml
````
or run the following command: 

````shell
bash <(curl -s -L https://raw.githubusercontent.com/snowdrop/k8s-infra/main/kind/kind-reg-ingress.sh)
````

This script creates a Kubernetes cluster using kind tool and deploys a private docker registry and Ingress controller NGINX to route the traffic

### Install the ingress controller

You can do it by running the following command:

````shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
````

Then, wait until is ready to process requests running:

````shell
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
````