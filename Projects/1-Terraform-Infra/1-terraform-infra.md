![image](https://github.com/user-attachments/assets/1d5417c5-cd70-4cf9-87a3-19b6956b44af)## Terraform with package installations
* Create a Terraform script to provision 3 virtual machines 
    * Make one vm as `JenkinsMaster` 
    * Other as `JenkinsSlave`
    * 3rd vm as `Ansible`
    * 4th vm as `sonar`
* Make sure the number of vms passed are dynamically, along with dynamic data. 
    * For example, jenkinsmaster might have t2.medium , Sonar might work with t2.micro
    * Hint: varibles, count, for_each, terraform.tfvars
* The same terraform script should be helping us to configure ansible contoller setup in the `Ansible` node 
* In output file, i should be having the details of the vm's created along with the port numbers as well.
```bash
jenkins_master = <publicip>:8080
nexus_server = <publivip>:8081
sonar_server = <publicip>:9000
```


step-1:

 version.tf

 variables.tf

 terraform.tfvars

terraform {
  required_version = ">= 1.2.0"
  #terraform providers required
  required_providers {
    aws = {
      #version = ">= 5.1.0"
      version = "~>4.47.0"
      source  = "hashicorp/aws"
    }
  }
}
provider "aws" {
  region  = "ap-southeast-1"
  profile = "default" #credentials taken from ~/.aws/configure
}

variable "vpc_cidr_blocks" {}
variable "subnet_cidr_blocks" {}
variable "availability_zone" {}
variable "public_ip" {}
variable "env_prefix" {}
variable "instances_configs" {}

vpc_cidr_blocks = "10.0.0.0/16"
subnet_cidr_blocks = "10.0.10.0/24"
availability_zone = "us-east-1a"
public_ip = "0.0.0.0/0"
env_prefix = "dev"
instances_configs = {
  jenkins-master = {
    ami_id = "ami-05c51de0bfac7492a"
    instance_type = "t2.micro"
    key_name  = "project-key"
  }
  jenkins-slave = {
    ami_id = "ami-05c51de0bfac7492a"
    instance_type = "t2.micro"
    key_name  = "project-key"
  }
  ansible-master = {
    ami_id = "ami-05c51de0bfac7492a"
    instance_type = "t2.micro"
    key_name  = "project-key"
  }
  
}
![image](https://github.com/user-attachments/assets/0ba8dacd-a218-4d35-b9de-28f48be33b29)
