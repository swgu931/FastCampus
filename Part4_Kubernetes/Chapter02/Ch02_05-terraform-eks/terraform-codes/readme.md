# Create EKS cluster by using Terraform
- precondition: VPC, Subnet, internet gateway, routing table 구성 완료

```
cd ./CH02_05-terraform-eks/terraform-codes

terraform init
terraform plan
terraform apply
```

- kube config setup for using kubectl
```
aws eks update-kubeconfig --region ap-northeast-2 --name test-eks-cluster
kubectl get nodes
kubectl describe no
```

# Delete EKS cluster by using Terraform

```
cd ./CH02_05-terraform-eks/terraform-codes
terraform plan --destroy
terraform destroy
```
