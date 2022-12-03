***How to Install Terraform on Ubuntu Server 20.04 Step by Step.***

$\Large{How \space to \space Install \space Terraform \space \space on \space Ubuntu \space Server \space 20.04 \space Step \space by \space Step.}$   

       
:arrow_down_small:

   :notes: [1. Install Terraform on Ubuntu 20.04 using APT :link:](#install_terraform)<br />
   :notes: [2. Install Terraform Manually :link: ](#install_terraform_manually)<br />
   :notes: [3. Install the "auto-complete" Terraform Extension :link:](#install_terraform_extension)<br />
   :notes: [4. Uninstall Terraform from Ubuntu 20.04 :link:](#uninstall_terraform)<br />
   :notes: [5. How to launch an EC2 instance using Terraform ? :link: ](#launch_instance)<br />    
       
        
What is Terraform ?

*Terraform is one of the popular open source infrastructure tools that is used as code software, first developed by HashiCorp Pvt. Ltd. Terraform is a user defined and data center infrastructure service provider that uses various HashiCorp languages, optionally it uses the JSON structure language rather than XML. The main purpose of using terraform platform is to build, change, and update the infrastructure functionality safely and effectively.*



Terraform is mainly divided into two parts, they are:

    - Terraform core
    - Terraform plugins


Advantages of Terraform (Pros)
    The terraform can be used as reproducible infrastructure management.    
    Reduces the production incident that arises due to environment configuration errors.
    Increases the velocity and reliability.
    Eliminates the wait time for environment provisioning.
    Helps in cleaning the work environment.
    The business benefits of defining infrastructure as code reduce the costs of system management and also lower the risk of unexpected problems that arise when modifications of infrastructure are implemented.



<a name="install_terraform"></a>                
:arrow_down: **1. Install Terraform on Ubuntu 20.04 using APT**

*APT also known as an “Advanced Packaging Tool” is a package manager for Debian based distributions. It allows you to install and manage packages on Debian and Ubuntu operating systems. In this section, we will show you how to install Terraform using apt.*

First, install the required dependencies using the following command:

    apt-get install wget curl unzip software-properties-common gnupg2 -y

Next, download and add the HashiCorp signed gpg keys to your system:

    curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -

Next, add the HashiCorp repository to the APT using the following command:

    apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

Next, update the repository using the command given below:

    apt-get update -y

Finally, install the Terraform by running the following command:

    apt-get install terraform -y

Once the Terraform has been installed, verify it using the following command:

    terraform -v

You will get the Terraform version in the following output:

    Terraform v1.1.2
    
on linux_amd64


<a name="install_terraform_manually"></a>
:arrow_down: **2. Install Terraform Manually**

*You can also install the Terraform manually by downloading it from the source. In this method, you can download the specific or latest version of Terraform to your system. You will also get the flexibility to install more than one version of Terraform.*

First, download the latest version of Terraform source using the following command:

    wget https://releases.hashicorp.com/terraform/1.1.2/terraform_1.1.2_linux_amd64.zip

Once the download is completed, extract the downloaded file using the following command.

    unzip terraform_1.1.2_linux_amd64.zip

Next, copy the Terraform binary from the extracted file to the /usr/bin/ directory:

    cp terraform /usr/bin/

Next, verify the Terraform version by running the following command:

    terraform -v

You will get the following output:

    Terraform v1.1.2
    
on linux_amd64


<a name="install_terraform_extension"></a>
:arrow_down: **3. Install the "auto-complete" Terraform Extension**

*Terraform provides auto-complete features that allow you to list all sub-commands after pressing the TAB key twice. In order to activate the auto-complete feature, you will need to install the autocomplete extension to your system. *

You can install it by running the following command:

    terraform -install-autocomplete

Next, run the following command to activate the auto-complete features:

    source ~/.bashrc

To check the Terraform auto-complete feature, run the terraform command and press the TAB key twice:

terraform


You should see all sub-commands in the following output:



apply         env           get           init          output        push          state         untaint       workspace
console       fmt           graph         login         plan          refresh       taint         validate
destroy       force-unlock  import        logout        providers     show          test          version


<a name="uninstall_terraform"></a>
:arrow_down: **4. Uninstall Terraform from Ubuntu 20.04**

If you want to remove Terraform from your system, run the following command:

    apt-get remove terraform -y

You can also remove it manually by running the following command:

    rm -rf /usr/bin/terraform



<a name="launch_instance"></a>
:arrow_down: **5. How to launch an EC2 instance using Terraform ?**


:arrow_forward: **Create an EC2 instance with Terraform**

***In this section, we'll write the code to create an EC2 instance. We'll review how to set up the main.tf file to create an EC2 instance and the variable files to ensure the instance is repeatable across any environment.***

Prerequisites:

    AWS account;
    AWS Identify and Access Management (IAM) credentials and programmatic access. The IAM credentials that you need for EC2 can be found here;
    setting up AWS credentials locally with aws configure in the AWS Command Line Interface (CLI). You can find further details here;
    a VPC configured for EC2. You can find a CloudFormation template to do that here; and
    a code or text editor.


:arrow_forward: **Step 1. Create the main.tf file**

***Open your text/code editor and create a new directory. Make a file called main.tf. When setting up the main.tf file, you will create and use the Terraform AWS provider -- a plugin that enables Terraform to communicate with the AWS platform -- and the EC2 instance.***

First, add the provider code to ensure you use the AWS provider.

      terraform {
        required_providers {
          aws = {
            source = "hashicorp/aws"
          }
        }
      }

***Next, set up your Terraform resource, which describes an infrastructure object, for the EC2 instance.  This will create the instance. Define the instance type and configure the network.***

      resource "aws_instance" "" {
        ami           = var.ami
        instance_type = var.instance_type

        network_interface {
          network_interface_id = var.network_interface_id
          device_index         = 0
        }

        credit_specification {
          cpu_credits = "unlimited"
        }
      }

:arrow_forward: **Step 2. Create the variables.tf file

***Once the main.tf file is created, it's time to set up the necessary variables. These variables let you pass in values, and ensure the code is repeatable. With variables, you can use your code within any EC2 environment.***

When setting up the variables.tf file, include the following three variables:

    The network interface ID to attach to the EC2 instance from the VPC.
    The Amazon Machine Image (AMI) of an instance. In the code snippet below, the AMI defaults to Ubuntu.
    The size of the instance. In the code snippet below, the instance type defaults to a t2 Micro instance size.

Within the variables.tf file, create the following variables:

      variable "network_interface_id" {
        type = string
        default = "network_id_from_aws"
      }

      variable "ami" {
          type = string
          default = "ami-005e54dee72cc1d00"
      }

      variable "instance_type" {
          type = string
          default = "t2.micro"
      }

:arrow_forward: **Step 3. Create the EC2 environment

To deploy the EC2 environment, ensure you're in the Terraform module/directory in which you write the Terraform code, and run the following commands:

    terraform init. Initializes the environment and pulls down the AWS provider.
    terraform plan. Creates an execution plan for the environment and confirm no bugs are found.
    terraform apply --auto-approve. Creates and automatically approves the environment.

:arrow_forward: **Step 4. Clean up the environment

To destroy all Terraform environments, ensure that you're in the Terraform module/directory that you used to create the EC2 instance and run terraform destroy.

:notebook: :pen:





















