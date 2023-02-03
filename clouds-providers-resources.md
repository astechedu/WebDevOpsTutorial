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









#
[Top](#top)
<a name="google-providers-resources"></a>
# Google Cloud Providers and Resources









#
[Top](#top)
<a name="azure-providers-resources"></a>
# Azure Cloud Providers and Resources








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













