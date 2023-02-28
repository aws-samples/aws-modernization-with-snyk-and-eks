---
title: "Create BitBucket Variables"
chapter: true
weight: 43 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

# Overview
Here we create repository variables to add details specific to your instance of the workshop.

## Repository variables

Next, you will need [repository variables](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/#Repository-variables) at the
repository level which will later be [referenced in your pipeline](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/).

These will consist of the following variables named as shown below:

1. Snyk API token for authenticating with your Snyk account: `SNYK_TOKEN`.  This is from your Snyk.io settings page.
1. AWS Identity & Access Management User [key and secret](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for secure authenticated interactions with the AWS API: `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`
1. AWS region you will be deploying to: `AWS_DEFAULT_REGION` with the value of something like `us-east-1`
1. Container image name: `IMAGE` with the value of "goof".  This name needs to match the name of your ECR.
1. Amazon EKS name of your cluster: `AWS_EKS_CLUSTER` if you have configured it.

This screenshot shows those repository variables:
![Repository Variables](/images/bitbucket-repo-vars.png)

{{% notice tip %}}
It is recommended that you use [Snyk Service accounts](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts) and [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) when creating accounts.
{{% /notice %}}
