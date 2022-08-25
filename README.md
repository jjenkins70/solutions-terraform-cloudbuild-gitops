# Managing infrastructure as code with Terraform, Cloud Build, and GitOps

This is the repo for the [Managing infrastructure as code with Terraform, Cloud Build, and GitOps](https://cloud.google.com/solutions/managing-infrastructure-as-code) tutorial. This tutorial explains how to manage infrastructure as code with Terraform and Cloud Build using the popular GitOps methodology. 

## Configuring your **dev** environment

Just for demostration, this step will:
 1. Configure an apache2 http server on network '**dev**' and subnet '**dev**-subnet-01'
 2. Open port 80 on firewall for this http server 

```bash
cd ../environments/dev
terraform init
terraform plan
terraform apply
terraform destroy
```

## Promoting your environment to **production**

Once you have tested your app (in this example an apache2 http server), you can promote your configuration to prodution. This step will:
 1. Configure an apache2 http server on network '**prod**' and subnet '**prod**-subnet-01'
 2. Open port 80 on firewall for this http server 

```bash
cd ../prod
terraform init
terraform plan
terraform apply
terraform destroy
```

## Suggested Pre-Requsites
- Create a demo project so you can easily destroy it later!
- Clone github repo (https://github.com/jjenkins70/solutions-terraform-cloudbuild-gitops)
- Configure Demo Project
    - `PROJECT_ID=$(gcloud config get-value project)`
    - `gcloud services enable cloudbuild.googleapis.com compute.googleapis.com`
git commands for CLI ease of use
```
git checkout -b new_branch (off of dev)
git remote add upstream https://github.com/jjenkins70/solutions-terraform-cloudbuild-gitops
git push -u origin new_branch
```


## After Demo
- Reset unique project ID to PROJECT_ID and push to git
```
cd ~/solutions-terraform-cloudbuild-gitops
sed -i s/$PROJECT_ID/PROJECT_ID/g environments/*/terraform.tfvars
sed -i s/$PROJECT_ID/PROJECT_ID/g environments/*/backend.tf
```
- Update modules/firewall/http-server to http-server2
Updated for live demo
