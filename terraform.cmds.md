## How to Install Terraform on Ubuntu Server 20.04 Step by Step.

:microphone:

   :notes: [1. Install Terraform on Ubuntu 20.04 using APT **click here** :link:](#install_terraform)<br />
   :notes: [2. Install Terraform Manually **click here** :link: ](#install_terraform_manually)<br />
   :notes: [3. Install the "auto-complete" Terraform Extension **click here** :link:](#install_terraform_extension)<br />
   :notes: [4. Uninstall Terraform from Ubuntu 20.04 **click here** :link:](#uninstall_terraform)<br />
        
What is Terraform ?

*Terraform is one of the popular open source infrastructure tools that is used as code software, first developed by HashiCorp Pvt. Ltd. Terraform is a user defined and data center infrastructure service provider that uses various HashiCorp languages, optionally it uses the JSON structure language rather than XML. The main purpose of using terraform platform is to build, change, and update the infrastructure functionality safely and effectively.*



Terraform is mainly divided into two parts, they are:

    Terraform core
    Terraform plugins


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


:notebook: :pen:
