# Terraform Configuration Language Syntax

## Step-01: Introduction
- Understand Terraform Language Basics
  - Understand Blocks
  - Understand Arguments, Attributes & Meta-Arguments
  - Understand Identifiers
  - Understand Comments
 


## Step-02: Terraform Configuration Language Syntax
- Understand Blocks
- Understand Arguments
- Understand Identifiers
- Understand Comments
- [Terraform Configuration](https://www.terraform.io/docs/configuration/index.html)
- [Terraform Configuration Syntax](https://www.terraform.io/docs/configuration/syntax.html)
```t
# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>"   {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}

# AWS Example
resource "aws_instance" "ec2demo" { # BLOCK
  ami           = "ami-04d29b6f966df1537" # Argument
  instance_type = var.instance_type # Argument with value as expression (Variable value replaced from varibales.tf
}
```
![image](https://user-images.githubusercontent.com/25415707/167358901-309069af-da80-42c5-9443-d4d895aedcfc.png)


![image](https://user-images.githubusercontent.com/25415707/167358947-e7d968d9-7255-427c-a47e-47225fbbcfa6.png)


![image](https://user-images.githubusercontent.com/25415707/167359050-a1d815a3-bdff-4049-8cb9-b51006c264e8.png)


![image](https://user-images.githubusercontent.com/25415707/167359166-514b992d-259b-401b-91b0-8ca789ce07fd.png)


![image](https://user-images.githubusercontent.com/25415707/167359204-c287b769-1a34-4643-bfbb-cb3c5be50418.png)


## Step-03: Understand about Arguments, Attributes and Meta-Arguments.
- Arguments can be `required` or `optional`
- Attribues format looks like `resource_type.resource_name.attribute_name`
- Meta-Arguments change a resource type's behavior (Example: count, for_each)
- [Additional Reference](https://learn.hashicorp.com/tutorials/terraform/resource?in=terraform/configuration-language) 
- [Resource: AWS Instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance)
- [Resource: AWS Instance Argument Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#argument-reference)
- [Resource: AWS Instance Attribute Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#attributes-reference)
- [Resource: Meta-Arguments](https://www.terraform.io/docs/language/meta-arguments/depends_on.html)


![image](https://user-images.githubusercontent.com/25415707/167360504-75e6da11-c384-4e9b-9052-39ced6aea0b7.png)

![image](https://user-images.githubusercontent.com/25415707/167360730-31861689-1f4b-4542-8311-e91c09c041af.png)

![image](https://user-images.githubusercontent.com/25415707/167360840-60f10d50-7b30-4c37-8cc7-21e686006d34.png)



## Step-04: Understand about Terraform Top-Level Blocks
- Discuss about Terraform Top-Level blocks
  - Terraform Settings Block
  - Provider Block
  - Resource Block
  - Input Variables Block
  - Output Values Block
  - Local Values Block
  - Data Sources Block
  - Modules Block


![image](https://user-images.githubusercontent.com/25415707/167361237-0aa530a7-592e-4788-bece-b85b6d523a06.png)



![image](https://user-images.githubusercontent.com/25415707/167361518-6efddb32-5402-48ef-a1ec-9271576eb1ff.png)







