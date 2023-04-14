---
title: "Create BitBucket Variables"
chapter: true
weight: 44 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

# Overview
Here we create [repository variables](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/#Repository-variables) to add details specific to your AWS and Snyk instances. These will later be [referenced in your pipeline](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/).

## Step 1: Enable Pipelines
From your Forked Repo, navigate to Repository Settings -> Pipelines -> Settings and enable pipelines.

![Enable Pipeline](/images/bitbucket-pipeline-enable.png)

## Step 2: Create Repository Variables
Under Repository Settings -> Pipelines, select Repository Variables. Create the following variables as shown below:

1. Snyk API token for authenticating with your Snyk account: `SNYK_TOKEN`.  This is from your Snyk.io settings page.
1. AWS Identity & Access Management User [key and secret](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for secure authenticated interactions with the AWS API: `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY` retrieved from the Event Engine dashboard.
1. AWS Session Token as `AWS_SESSION_TOKEN` also retrieved from the Event Engine dashboard.
1. AWS region you will be deploying to: `AWS_DEFAULT_REGION` with the value of `us-east-1`
1. Container image name: `IMAGE` with the value of "goof".  This name needs to match the name of your ECR.
1. The URI to your AWS ECR: `AWS_ECR_URI`.  We use this for the deployment to EKS.
1. (OPTIONAL) Amazon EKS name of your cluster: `AWS_EKS_CLUSTER` if you have configured it in a previous step.

This screenshot shows those repository variables:
![Repository Variables](/images/bitbucket-repo-vars.png)

{{% notice tip %}}
It is recommended that you use [Snyk Service accounts](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts) and [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) when creating accounts.
{{% /notice %}}

When finished, navigate back to the Repo's Source view.