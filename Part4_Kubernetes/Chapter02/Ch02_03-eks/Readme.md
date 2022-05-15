# AWS 웹 콘솔을 활용한 AWS EKS 생성 

## EKS Cluster 및 Nodegroup이 실행될 대상 Subnet에는 반드시 해당 TAG가 있어야함
- TAG명 : kubernetes.io/cluster/<EKS Cluster명>
- TAG값 : shared


## Console을 이용한 클러스터 생성 순서

```
EKS cluster 생성 이름 : test-eks-cluster


VPC 1개
subnet 2개 
  tag :  kubernetes.io/cluster/test-eks-cluster

Security Group 설정
IAM role 설정 (custom 추가)
---
{
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Principal": {
            "Service": "eks.amazonaws.com"
        },
        "Action": "sts:AssumeRole"
        }
    ]
}
---
IAM nodegroup role 설정 (custom 추가)
---
{
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Principal": {
            "Service": "ec2.amazonaws.com"
        },
        "Action": "sts:AssumeRole"
        }
    ]
}
---
EKS 생성

nodegroup 생성
 : test-aim-role-eks-nodegroup 연결

 : nodegroup 컴퓨팅 구성
    - 워커노드 2개
       (최소 1개, 최대 3개)
 
```
## kubectl install
```
curl -o kubectl https://amazon-eks.s3.us-west-
2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

chmod +x ./kubectl && mv ./kubectl /usr/local/bin/

kubectl versino
```

## aws cli
```
# 1. AWS 계정 Access Key 설
aws configure

# 2. Kubectl 사용을 위한 Kubeconfig 설정
aws eks update-kubeconfig --region <Region명> --name <EKS명>
```
