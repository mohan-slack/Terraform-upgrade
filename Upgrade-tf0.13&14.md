git branch

git checkout -B "upgrade/terraform0.13"

echo "latest:^0.13" > .terraform-version

Update the module version references to the latest 3.x.x module version; ie/ `.git?ref=3.0.0`, and ensure that each module uses the 
public git URL base: `git::ssh://git@code.pruconnect.net:7999`

Update the provider version constraints, specifically: azurerm = "~> 2.0"; add the `features {}` block to the azurerm provider
    versions.tf
        terraform version 0.12--->0.13
        azurerm = "~> 3.0"

terraform init -backend=false

terraform 0.13upgrade -yes
terraform validate
tflint

Push the branch and create a Pull Request; review and ensure that any planned changes are desired
git add .
git commit -m "tf0.13 upgrade"
git push -u origin upgrade/terraform0.13 --force


===================================================
=======================================================
====================================================
git checkout master

git pull origin master

terraform version
Terraform v0.13.7

git checkout -B "upgrade/terraform0.14"

echo "latest:^0.14" > .terraform-version

versions.tf & init.tf==> change version from 0.13-0.14

.tflint.hcl --> add this file

terraform init -backend=false

terraform validate

tflint

Push the branch and create a Pull Request; review and ensure that any planned changes are desired
git add .
git commit -m "tf0.14 upgrade"
git push -u origin upgrade/terraform0.14 --force

