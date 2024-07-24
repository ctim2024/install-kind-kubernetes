# install-kind-kubernetes
this repo describe how to install kind utility

## Install kind

```bash
choco install kind
```
## Create new cluster

```bash
kind create cluster --config cluster-config.yaml
```

## Install dashboard (Optional)

```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
   kubectl apply -f dashboard-adminuser.yaml -n kubernetes-dashboard
   kubectl apply -f dashboard-clusterrole.yaml -n kubernetes-dashboard
   kubectl apply -f dashboard-secret.yaml -n kubernetes-dashboard
   kubectl apply -f dashboard-nodeport.yaml -n kubernetes-dashboard
   #execute on git bash :
   kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath={".data.token"} | base64 -d
```

## Install ingress (Optional)

```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
   kubectl edit deployment ingress-nginx-controller -n ingress-nginx
```
   delete this section :
                         nodeSelector:
                             ingress-ready: "true"