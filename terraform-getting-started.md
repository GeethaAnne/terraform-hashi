# Getting Started with Terraform

Terraform is the most popular langauge for defining and provisioning infrastructure as code (IaC). It uses the declarative language HCL (HashiCorp Configuration Language) to define infrastructure as code.

# What is infrastructure as code?
Infrastructure as Code, in simple terms, is a means by which you can write declarative definitions for the infrastructure you want to exist and using them with a provisioning tool that deals with the actual deployment. This means that we can code what we want built, provide necessary credentials for the given IaaS provider, kick off the provisioning process and come back to find all your services purring along nicely in the cloud

In this tutorial, we will introduce the basics of how to use Terraform to define and manage your infrastructure.

# Prerequisites
To install Terraform, simply visit [Terraform.io](https://www.terraform.io/downloads.html) and download the compressed binary application executable file deliverable for your platform, machine or environment on which you like to run code and do development.


With Terraform installed, let's dive right into it and start creating some infrastructure.

 # Create a Working Directory
Most users find it convinient to create a new directory on there local machine and create Terraform configuration code inside it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```
# Create Terrform 
Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command. The Docker provider will be installed. 

```shell
$ terraform init
```

You shoud check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message are the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.
