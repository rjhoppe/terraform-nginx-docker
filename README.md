# Provisioning a Docker NGINX Container with Terraform

## Technologies
* Terraform
* NGINX
* Docker
* WSL
* Windows

## Description

Followed along with Terraform tutorial here: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Provisioned an NGINX server running locally on a Windows machine using Terraform. However, what I did to make the deployment work, varied from what was explained on the HashiCorp whitepapers. 

I needed to remove the following declarations from my main.tf file:

```
provider "docker" {
  host    = "npipe:////.//pipe//docker_engine"
}
```

You also MUST have Docker currently running locally on your machine. If Docker is installed, but not running you will receive an error when you go to run your 'terraform plan' or 'terraform apply' cmds

Here are some errors you can run into if you have previous declarations in your main.tf file or if you don't have Docker running locally:

```
│ Error: Error initializing Docker client: protocol not available
│
│   with provider["registry.terraform.io/kreuzwerker/docker"],
│   on main.tf line 11, in provider "docker":
│   11: provider "docker" {
```

OR

```
│ Error: Error pinging Docker server: Cannot connect to the Docker daemon at unix:///var/run/docker.so
│
│   with provider["registry.terraform.io/kreuzwerker/docker"],
│   on main.tf line 11, in provider "docker":
│   11: provider "docker" {
```

