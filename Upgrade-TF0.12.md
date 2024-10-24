Steps:
tfenv use latest:^0.11
================
tfenv list
================
tfenv --version
================
terraform version
Terraform v0.11.15
================
git branch
* master
=================
git checkout -B "upgrade/terraform0.12"
Switched to a new branch 'upgrade/terraform0.12'
=================
git branch
  master
* upgrade/terraform0.12
===================
Note: change vault version to 2.0 if in use (look at init.tf or versions,tf file)
====================
terraform init -backend=false
====================
add new file:
.terraform-version  --> latest:^0.12  (Make sure no spaces before . or anyplace-caseSensitive File Name)
======================
terraform 0.12upgrade -yes
========
Remove version-1.tf file and add below content into versions.tf file after 0.12 version upgrade
======================
terraform {
  required_version = "~> 0.12"

  backend "azurerm" {}
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 2.0"
    }
    
    azuread = {
      source  = "hashicorp/azuread"
      version = "~> 1.0"
    }
    
    vault = {
      source  = "hashicorp/vault"
      version = "~> 2.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "~> 3.0"
    }
 }
}

provider "azurerm" {
  features {}
}

provider "azurerm" {
  alias           = "hub"
  subscription_id = var.hub_subscription_id
  features {}
}
====================
rm -rf .terraform 
Create below files: (Get the file from this folder)
.gitignore
====================
#Check for the source files in main.tf/VM.tf files and changes module versions which are compatible with 0.12 versions.
#How to check:
#https://code.pruconnect.net/projects/RTSRETM
#search "application-security-group" (Module name)
#select "changeLog.md" and check compatible version for 0.12 
  Ex:
     2.0.0
      updated for terraform 0.12 
#switch Master-> 2.0.0 tag -> cross check versions.tf file to confirm 0.12 & provider versions are compatible and needs to change.
#Update same in source in BP .tf files
#variables.tf -> map/map(string)----->>>map(any)

====================
terraform init -backend=false
====================
terraform validate
====================
tflint (ignore for warnings for now)
====================
git add .
git commit -m "tf0.12 upgrade"
git push -u origin upgrade/terraform0.12 --force

======================================================================

