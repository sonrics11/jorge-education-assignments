# Getting Started with Terraform

This guide shows you how to install Terraform, create your first infrastructure configuration, and manage the lifecycle of Docker resources using Terraform.

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running
- Command-line interface (CLI) access

## Install Terraform

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the appropriate binary for your platform.

## Create a working directory

Create a new directory on your local machine for your Terraform configuration code.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

## Write the configuration

Create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
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

## Initialize Terraform

Initialize Terraform with the `init` command. You will donwload nginx image and deploy a container.

```shell
$ terraform init
```

Check for any errors. If it ran successfully, proceed to the next step.

## Provision the resource

Provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource are created.

## Destroy the infrastructure

Destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it created earlier.

## Next steps

In this guide, you installed Terraform, wrote a configuration to deploy a Docker container, and managed the complete lifecycle of Docker resources using Terraform commands. You learned how to initialize a Terraform project, apply configurations to create resources, and destroy resources when they are no longer needed.

To continue learning about Terraform, explore the following resources:

- [Terraform Documentation](https://www.terraform.io/docs) - Learn about Terraform's features and capabilities
- [Terraform Tutorials](https://learn.hashicorp.com/terraform) - Follow step-by-step tutorials for different use cases
- [Terraform Providers](https://registry.terraform.io/browse/providers) - Discover providers for AWS, Azure, GCP, and other platforms
