# Terraformer
- ref : https://github.com/GoogleCloudPlatform/terraformer/blob/master/docs/aws.md

## S3 및 DynamoDB table 생성
```
cd ./terraform-backend
terraform init
terraform plan
terraform apply
```

## terraform state 파일 업로드 to S3
```
cd ../Ch02_05-terraform-eks/terraform-codes/
aws s3 cp terraform.tfstate s3://test-s3-tf-state/terraform.tfstate
```

## Nodegroup 생성 by Reverse Engineering
- EC2 > 시작 템플릿
- EC2 > Auto Scaling group

```
terraformer version
cd ../terraformer
terraformer import aws --regions=ap-northeast-2 --resources=auto_scaling --path-parttern=auto_scaling
terraform init
ls -a
terraformer import aws --regions=ap-northeast-2 --resources=auto_scaling --path-parttern=auto_scaling
cd auto_scaling
cat auto_scaling.tf
cat launch_template.tf
cat output.tf
cat provider.tf
cat terraform.tfstate
cat variables.tf
cat .terraform.lock.hcl
terraform state list
```
```
cd ..
ls
aws s3 cp s3://test-s3-tf-state/terraform.tfstate ./
terraform state list
```
```
cd auto_scaling
#  terraform state mv -state-out=<기존 Terraform Backend 상태파일 저장 경로> <추출Terraform Object명> <Import되서 저장될 Terraform Object명>
terraform state mv -state-out=../terraform.tfstate aws aws_autoscaling_group.tfer--eks-test-eks-nodegroup-7ebxxx765 aws_autoscaling_group.tfer--eks-test-eks-nodegroup-7ebxxx765

terraform state mv -state-out=../terraform.tfstate aws aws_launch_template.tfer--eks-test-eks-7ebxxx765 aws_launch_template.tfer--eks-test-eks-7ebxxx765

cd ..
ls
terraform state list

aws s3 cp terraform.tfstate s3://test-s3-tf-state/terraform.tfstate

```
```
cp ./terraformer/autoscaling/autoscaling_group.tf ./terraform-code/
cp ./terraformer/autoscaling/launch_template.tf ./terraform-code/
```
```
vi ./terraform-codes/eks-nodegroup.tf
# nodegroup2 로 추가
# launch_template 추가

vi ././terraform-codes/launch_template.tf
# iam_instance_template 주석처리
```
```
cd terraform-codes
vi provider.tf   # 수정
terraform init
terraform plan
terraform apply
kubectl get node
```

## Network
```
cd terraformer
ls
rm terraform.tfstate*

terraformer import aws --regions=ap-northeast-2 --resouces=vpc --path--pattern=vpc

terraformer import aws --regions=ap-northeast-2 --resouces=subnet --path--pattern=subnet

terraformer import aws --regions=ap-northeast-2 --resouces=igw --path--pattern=igw

terraformer import aws --regions=ap-northeast-2 --resouces=route_table --path--pattern=route_table

aws s3 cp s3://test-s3-tf-state/terraform.tfstate ./
ls

cd igw
ls
terraform state list
terraform state mv -state-out=../terraform.tfstate aws_internet_gateway.tfer--igw-009933xxx aws_internet_gateway.tfer--igw-009933xxx
cd route_table
terraform state list
terraform state mv -state-out=../terraform.tfstate aws_route_table.tfer--igw-009933xxx aws_route_table.tfer--igw-009933xxx
# route_table 은 6개에 대해 실행

cd subnet
terraform state list
terraform state mv ...

cd vpc
terraform state list
terraform state mv ....

aws s3 cp terraform.tfstate s3://test-s3-tf-state/terraform.tfstate

cp ..
cp ./igw/internet_gateway.tf   ../terraform-codes/
cp ./route_table/main_route_table_association.tf   ../terraform-codes/
cp ./route_table/route_table_association.tf   ../terraform-codes/
cp ./route_table/route_table.tf   ../terraform-codes/
cp ./subnet/subnet.tf ../terraform-codes/
cp ./vpc/vpc.tf ../terraform-codes/
```
```
cd ..
ls
cd terraform-codes
terraform init
# lock 으로 인해 error -> DynamoDB 의 table에 가서 lockID 삭제
terraform init
# Invalid legacy provide address 으로 인해 error
terraform state replace-provider -auto-approve registry.terraform.io/-/aws hashicorp/aws
terraform init
terraform plan
terraform apply
```





