Using this repo to try out the new MarkLogic 1.0.0 Helm chart.

Things I did to get setup:
- Used instructions at https://matthewpalmer.net/kubernetes-app-developer/articles/guide-install-kubernetes-mac.html 
- Already had Docker installed; updated it to 4.18.0
- `brew install kubectl`
- `brew install minikube`
- `brew install kubernetes-helm`

Then went to https://github.com/marklogic/marklogic-kubernetes , installed the chart:

helm repo add marklogic https://marklogic.github.io/marklogic-kubernetes/

And then the following instructions successfully created a single-node cluster:

```
kubectl create namespace marklogic
kubectl create secret generic ml-admin-secrets --from-literal=username='admin' --from-literal=password='admin' --from-literal=wallet-password='admin' --namespace=marklogic
helm install my-release marklogic/marklogic --version=1.0.0 --values values.yaml --namespace=marklogic
```

Was able to enable port-forwarding via the following:

    kubectl port-forward my-release-marklogic-0 8000 8001 8002 8016

And I was then able to deploy an app onto MarkLogic with a REST API instance on port 8016.