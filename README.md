# HELLO WORLD TERRAFORM

```hlc

terraform {
  required_providers {
    docker = {
        source = "kreuzwerker/docker"
        version = "~> 3.0.1"
    }
  }
}


provider "docker" {}

resource "docker_image" "nginx" {
    name      = "nginx:lastest"
    keep_locally = false
}

resource "docker_container" "nginx"{
    image = docker_image.nginx.image_id
    name  = "tutorial"
    ports {
        internal = 80
        external = 8000
    }
}

```
## Terraform Block

The ``` terraform {}``` block contains Terraform settings, including the required providers Terraform will use to provision your infrastructure. For each provider, the source attribute defines an optional hostname, a namespace, and the provider type. Terraform installs providers from the Terraform Registry by default. In this example configuration, the docker provider's source is defined as kreuzwerker/docker, which is shorthand for registry.terraform.io/kreuzwerker/docker.

## Providers
The ``` provider``` block configures the specified provider, in this case docker. A provider is a plugin that Terraform uses to create and manage your resources.

You can use multiple provider blocks in your Terraform configuration to manage resources from different providers. You can even use different providers together. For example, you could pass the Docker image ID to a Kubernetes service.

## Resources
Use ``` resource``` blocks to define components of your infrastructure. A resource might be a physical or virtual component such as a Docker container. Resource blocks have two strings before the block: the resource type and the resource name. 

In this example, the first resource type is ``` docker_image ``` and the name is ``` nginx```.

The prefix of the type maps to the name of the provider. In the example configuration, Terraform manages the ``` docker_image ``` resource with the ``` docker ``` provider. Together, the resource type and resource name form a unique ID for the resource. For example, the ID for your Docker image is ``` docker_image.nginx ```.

Resource blocks contain arguments which you use to configure the resource. Arguments can include things like machine sizes, disk image names, or VPC IDs. For your container, the example configuration sets the Docker image as the image source for your ``` docker_container``` resource.

## Steps

```hlc
terraform init
terraform fmt
terraform validate
```
## Create infrastructure;

```hlc
terraform apply
```