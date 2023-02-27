---
title: "Create ECR"
chapter: true
weight: 42 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

# Overview
Here we create an Amazon Elastic Container Registry for your containers.

## Setup

Before you can push your images to Amazon ECR, you must [create a repository](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html) to store them in. You can create Amazon ECR repositories with the AWS Management Console, or with the AWS CLI and AWS SDKs.
For this workshop, we will create the repository with the AWS Management Console:

1. Open the Amazon ECR console at https://console.aws.amazon.com/ecr/repositories.
1. From the navigation bar, choose the Region to create your repository in.
1. In the navigation pane, choose Repositories.
1. On the Repositories page, choose Create repository.
1. For Repository name, enter a unique name for your repository.  For the purpose of this workshop, we'll call it `goof`
1. For Tag immutability, choose the tag mutability setting for the repository. Repositories configured with immutable tags will prevent image tags from being overwritten. For more information, see Image tag mutability.
1. For Scan on push, choose the image scanning setting for the repository. Repositories configured to scan on push will start an image scan whenever an image is pushed, otherwise image scans need to be started manually. For more information, see Image scanning.
1. Choose Create repository.
