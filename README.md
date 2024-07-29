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

## Install ingress (Optional)

```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
   
```

```bash
     kubectl edit deployment ingress-nginx-controller -n ingress-nginx

       delete this section :
                            nodeSelector:
                              ingress-ready: "true"
```

## Install dashboard (Optional)

### Create yaml dashborad 
```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```
### Create ServiceAccount
```bash
   kubectl apply -f dashboard-adminuser.yaml -n kubernetes-dashboard
```
### Create the role
```bash   
   kubectl apply -f dashboard-clusterrole.yaml -n kubernetes-dashboard
```
### Create the secret
```bash   
   kubectl apply -f dashboard-secret.yaml -n kubernetes-dashboard
```
### Create the service resource
```bash   
   kubectl apply -f dashboard-nodeport.yaml -n kubernetes-dashboard
```
### Create ingress resource to access dashboard from the host
```bash   
   kubectl apply -f ingress-dashboard.yaml -n kubernetes-dashboard
```
### Get the secret
```bash   
   #execute on git bash :
   kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath={".data.token"} | base64 -d
```


