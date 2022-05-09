# Terraform Basic Blocks

![image](https://user-images.githubusercontent.com/25415707/167407884-4be3b490-ced8-4c41-a3a5-85b56e02cc4f.png)


![image](https://user-images.githubusercontent.com/25415707/167408095-b9b7082c-fe69-491a-b4cb-0ff6ef4b0d2d.png)


![image](https://user-images.githubusercontent.com/25415707/167408198-e39ea5d9-a0ac-482d-8d9d-11d96a451503.png)


![image](https://user-images.githubusercontent.com/25415707/167408587-fff584ff-199e-4319-80bf-d5d85ab155bd.png)


![image](https://user-images.githubusercontent.com/25415707/167408643-7142b944-447a-4c27-a173-d04cd1c36572.png)


![image](https://user-images.githubusercontent.com/25415707/167408763-1035e2dd-4de2-4d4c-b98e-0fe67f3c0c92.png)


![image](https://user-images.githubusercontent.com/25415707/167408964-eb69e0a7-ceaa-4a30-b48f-ac8ca0872d2a.png)


![image](https://user-images.githubusercontent.com/25415707/167409064-5fa26736-f6f3-4896-b76c-c20babc0d46c.png)


![image](https://user-images.githubusercontent.com/25415707/167409458-b73667ef-5476-4de3-acd0-2e08290d6fec.png)


![image](https://user-images.githubusercontent.com/25415707/167409541-141a7178-a377-4ed0-b20f-8c85348eb239.png)


![image](https://user-images.githubusercontent.com/25415707/167436446-e707da3e-0cc7-4070-bcbf-9c0e2bfc5521.png)


![image](https://user-images.githubusercontent.com/25415707/167436484-5d020956-c7fe-4be9-85e8-80a14d6c62ec.png)


## Argument Reference : Inputs that are given
## Attribute Reference : Values that can be exported for the resources

![image](https://user-images.githubusercontent.com/25415707/167437300-2e75fd29-4688-4cc9-bfe2-b192a788a4eb.png)

------------------------------------------------------------------------------------------------------------------------------------------------------------


## Terraform State

![image](https://user-images.githubusercontent.com/25415707/167437852-4313a663-fbbf-4395-b25c-34605a8b91c4.png)

![image](https://user-images.githubusercontent.com/25415707/167437913-e6f6386d-9815-4ff4-8fc3-cf62262f7d81.png)


------------------------------------------------------------------------------------------------------------------------------------------------------------

# Terraform Settings, Providers & Resource Blocks
## Step-01: Introduction
- [Terraform Settings](https://www.terraform.io/docs/language/settings/index.html)
- [Terraform Providers](https://www.terraform.io/docs/providers/index.html)
- [Terraform Resources](https://www.terraform.io/docs/language/resources/index.html)
- [Terraform File Function](https://www.terraform.io/docs/language/functions/file.html)
- Create EC2 Instance using Terraform and provision a webserver with userdata. 

## Step-02: In c1-versions.tf - Create Terraform Settings Block
- Understand about [Terraform Settings Block](https://www.terraform.io/docs/language/settings/index.html) and create it
```t
terraform {
  required_version = "~> 0.14" # which means any version equal & above 0.14 like 0.15, 0.16 etc and < 1.xx
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}
```

## Step-03: In c1-versions.tf - Create Terraform Providers Block 
- Understand about [Terraform Providers](https://www.terraform.io/docs/providers/index.html)
- Configure AWS Credentials in the AWS CLI if not configured
```t
# Verify AWS Credentials
cat $HOME/.aws/credentials
```
- Create [AWS Providers Block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication)
```t
# Provider Block
provider "aws" {
  region  = us-east-1
  profile = "default"
}
```

## Step-04: In c2-ec2instance.tf -  Create Resource Block
- Understand about [Resources](https://www.terraform.io/docs/language/resources/index.html)
- Create [EC2 Instance Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance)
- Understand about [File Function](https://www.terraform.io/docs/language/functions/file.html)
- Understand about [Resources - Argument Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#argument-reference)
- Understand about [Resources - Attribute Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#attributes-reference)
```t
# Resource: EC2 Instance
resource "aws_instance" "myec2vm" {
  ami = "ami-0533f2ba8a1995cf9"
  instance_type = "t3.micro"
  user_data = file("${path.module}/app1-install.sh")
  tags = {
    "Name" = "EC2 Demo"
  }
}
```


## Step-05: Review file app1-install.sh
```sh
#! /bin/bash
# Instance Identity Metadata Reference - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-identity-documents.html
sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo service httpd start  
sudo echo '<h1>Welcome to StackSimplify - APP-1</h1>' | sudo tee /var/www/html/index.html
sudo mkdir /var/www/html/app1
sudo echo '<!DOCTYPE html> <html> <body style="background-color:rgb(250, 210, 210);"> <h1>Welcome to Stack Simplify - APP-1</h1> <p>Terraform Demo</p> <p>Application Version: V1</p> </body></html>' | sudo tee /var/www/html/app1/index.html
sudo curl http://169.254.169.254/latest/dynamic/instance-identity/document -o /var/www/html/app1/metadata.html
```

## Step-06: Execute Terraform Commands
```t
# Terraform Initialize
terraform init
Observation:
1) Initialized Local Backend
2) Downloaded the provider plugins (initialized plugins)
3) Review the folder structure ".terraform folder"

# Terraform Validate
terraform validate
Observation:
1) If any changes to files, those will come as printed in stdout (those file names will be printed in CLI)

# Terraform Plan
terraform plan
Observation:
1) No changes - Just prints the execution plan

# Terraform Apply
terraform apply 
[or]
terraform apply -auto-approve
Observations:
1) Create resources on cloud
2) Created terraform.tfstate file when you run the terraform apply command
```

## Step-07: Access Application
- **Important Note:** verify if default VPC security group has a rule to allow port 80
```t
# Access index.html
http://<PUBLIC-IP>/index.html
http://<PUBLIC-IP>/app1/index.html

# Access metadata.html
http://<PUBLIC-IP>/app1/metadata.html
```

## Step-08: Terraform State - Basics
- Understand about Terraform State
- Terraform State file `terraform.tfstate`
- Understand about `Desired State` and `Current State`


## Step-09: Clean-Up
```t
# Terraform Destroy
terraform plan -destroy  # You can view destroy plan using this command
terraform destroy

# Clean-Up Files
rm -rf .terraform*
rm -rf terraform.tfstate*
```


## Step-10: Additional Observations - Concepts we will learn in next section
- EC2 Instance created we didn't associate a EC2 Key pair to login to EC2 Instance 
  - Terraform Resource Argument - `Key Name`
- AMI Name is static - How to make it Dynamic ?
  - Use `Terraform Datasources` concept
- We didn't create multiple instances of same EC2 Instance
  - Resource Meta-Argument: `count` 
- We didn't add any variables for parameterizations
  - Terraform `Input Variable` Basics
- We didn't extract any information on terminal about instance information 
  -  Terraform `Outputs`
- Create second resource only after first resource is created
  - Defining Explicit Dependency in Terraform using Resource Meta-Argument `depends_on`
- WE ARE GOING TO LEARN ALL THE ABOVE CONCEPTS IN NEXT SECTION
