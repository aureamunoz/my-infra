# Set up infra using Kind

### Install Kind with ingress controller and internal registry

Run the following command: 

````shell
bash <(curl -s -L https://raw.githubusercontent.com/snowdrop/k8s-infra/main/kind/kind-reg-ingress.sh)
````

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
kubectx kind-kind
````

`kubectx` will show the available contexts.


## Usando quickstart kind

https://knative.dev/docs/getting-started/quickstart-install/#install-the-knative-quickstart-plugin

and

https://knative.dev/docs/getting-started/first-service/

##### Some used links:

https://knative.dev/docs/getting-started/quickstart-install/
https://rohaan.medium.com/accessing-knative-rest-api-using-fabric8-knative-client-443a16ac43f7
https://github.com/fabric8io/kubernetes-client/issues/2354

