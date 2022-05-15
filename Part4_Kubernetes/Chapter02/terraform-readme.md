# Create EKS cluster by Terraform
- ref: https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code

## Install Terraform
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
```

Or

```
wget https://releases.hashicorp.com/terraform/1.1.9/terraform_1.1.9_linux_amd64.zip
unzip terraform_1.1.9_linux_amd64.zip
sudo mv ./terraform /usr/local/bin/
```

## Reference
- resources
- data sources
- providers
- variables
```
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster

https://registry.terraform.io/browse/providers

https://www.terraform.io/language/values/variables
```

## Basic Command
```
terraform init
terraform plan  # Dry Run
terraform apply 
terraform plan --destroy  # Dry Run
terraform destroy
```
