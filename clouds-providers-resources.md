$$\color{purple}{Clouds \ : Providers \ And \ Resources}$$


[Home](#all-file-links.md)
<a name="top"></a>

Topics: 

  [Terrafomr Registery io: providers and resources list](https://registry.terraform.io/)
 
  1. [AWS Cloud Providers and Resources](#aws-providers-resources)
   
  2. [Google Cloud Providers and Resources](#google-providers-resources)
   
  3. [Azure Cloud Providers and Resources](#azure-providers-resources)
    
  4. [Github Cloud Providers and Resources](#github-providers-resources)
    
              
        
    
    
   
   
    
    
    
    
    
#
[Top](#top)
<a name="aws-providers-resources"></a>
# AWS Cloud Providers and Resources

How to use this provider?

To install this provider, copy and paste this code into your Terraform configuration. Then, run terraform init.

Terraform 0.13+

Provider:


      terraform {
        required_providers {
          aws = {
            source = "hashicorp/aws"
            version = "4.53.0"
          }
        }
      }

      provider "aws" {
        # Configuration options
      }




Resources:

Example Usage


    data "aws_instance" "foo" {
      instance_id = "i-instanceid"

      filter {
        name   = "image-id"
        values = ["ami-xxxxxxxx"]
      }

      filter {
        name   = "tag:Name"
        values = ["instance-name-tag"]
      }
    }




#
[Top](#top)
<a name="google-providers-resources"></a>
# Google Cloud Providers and Resources



How to use this provider

To install this provider, copy and paste this code into your Terraform configuration. Then, run terraform init.

Terraform 0.13+


Provider:


    terraform {
      required_providers {
        google = {
          source = "hashicorp/google"
          version = "4.51.0"
        }
      }
    }

    provider "google" {
      # Configuration options
    }



Resources:


Example Usage - Dns Managed Zone


    resource "google_dns_managed_zone" "example-zone" {
      name        = "example-zone"
      dns_name    = "example-${random_id.rnd.hex}.com."
      description = "Example DNS zone"
      labels = {
        foo = "bar"
      }
    }

    resource "random_id" "rnd" {
      byte_length = 4
    }




#
[Top](#top)
<a name="azure-providers-resources"></a>
# Azure Cloud Providers and Resources


How to use this provider

To install this provider, copy and paste this code into your Terraform configuration. Then, run terraform init.

Terraform 0.13+


Provider:



    terraform {
      required_providers {
        azurerm = {
          source = "hashicorp/azurerm"
          version = "3.41.0"
        }
      }
    }

    provider "azurerm" {
      # Configuration options
    }



Resources: 

Example Usage

    resource "azurerm_kubernetes_fleet_manager" "example" {

      hub_profile {
        dns_prefix = "example"
      }

      location            = azurerm_resource_group.example.location
      name                = "example"
      resource_group_name = azurerm_resource_group.example.name
    }




#
[Top](#top)
<a name="github-providers-resources"></a>
# Github Cloud Providers and Resources


How to use this provider

To install this provider, copy and paste this code into your Terraform configuration. Then, run terraform init.

Terraform 0.13+

Provider: 

[Github Provider Link](https://registry.terraform.io/providers/integrations/github/5.16.0)


          terraform {
            required_providers {
            
              github = {
                source = "integrations/github"
                version = "5.16.0"
              }
            }
          }

          provider "github" {
            # Configuration options
          }


Resource:

[Github Resources Link](https://registry.terraform.io/providers/integrations/github/latest/docs)


Example Usage:

          resource "github_repository" "example" {
            name        = "example"
            description = "My awesome codebase"

            visibility = "public"

            template {
              owner                = "github"
              repository           = "terraform-template-module"
              include_all_branches = true
            }
          }













