# Helm command

## helm basic command
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

```
helm uninstall nginx
helm ls
```

## helm custom
```
helm create test
cd test
tree
```

## helm grammer  
```
helm lint .
helm list
helm ls
helm template .
# 출력내용을 manifext.yaml 을 만들어서 복사
# manifext.yaml 읠 RELEASE-NAME 을 nginx 로 치환
kubectl create -f manifest.yaml
kubectl get all
kubectl get po
kubectl logs [pod-name]
kubectl delete -f manifest.yaml
kubectl get all

helm ls
helm package test
mkdir temp
mv *.tgz temp/
cd temp
ls
tar xvfz nginx-9.9.0.tgz
ls 
cd nginx

tar xvfz test-0.1.0.tgz
ls 
cd test
vi values.yaml
```

```
cd ../../test
ls
helm install nginx .
helm ls
kubectl get all
helm test nginx
kubectl get po
kubectl logs [pod-name]
```
```
cd template
cat NOTES.txt
cat chart.yaml

cd test
helm show chart .
helm show all .

helm template .
helm status nginx

vi deployment.yaml
helm template .
vi _helpers.tpl

kubectl get deploy # _helpers.tpl 과 values.yaml 을 비교해서 값은 취함

vi ../values.yaml

# hpa enalbe 후에 upgrade
helm upgrade nginx .
kubectl get all

```
