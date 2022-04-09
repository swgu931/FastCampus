# Helm command

```
helm ls
kubectl get all
helm repo add stable https://charts.helm.sh/stable
helm repo list
helm repo add test-repo https://charts.bitnami.com/bitnami
helm repo remove test-repo
helm repo add test-repo https://charts.bitnami.com/bitnami

helm search repo nginx
helm repo update
helm search repo nginx

helm install nginx test-repo/nginx --version 9.9.0
helm ls
helm status nginx

helm upgrade nginx test-repo/nginx --version 9.9.3
helm ls

helm history nginx
kubectl get all

helm rollback nginx 1
helm ls
helm history nginx
kubectl get all
ls

helm fetch --untar test-repo/nginx --versino 9.9.0
ls
cd nginx
```
