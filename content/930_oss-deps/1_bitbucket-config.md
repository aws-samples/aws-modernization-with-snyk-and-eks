+++
title = "Bitbucket Configuration"
chapter = false
weight = 1
+++

In this section, we'll configure Snyk to have access to your Bitbucket environment.  This requires you to create a Personal Access Token on Bitbucket which we'll use in Snyk.


## Create a Bitbucket App Password

You will need to [create an app password](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/) in order to 
authorize Snyk to access your repository and enable Snyk's [Bitbucket Cloud integration](https://support.snyk.io/hc/en-us/articles/360004032097-Bitbucket-Cloud-integration).

To create an app password:

1. From your avatar in the bottom left, click __Personal settings__.
1. Click __App passwords__ under __Access management__.
1. Click __Create app password__.
1. Give the app password a name related to the application that will use the password.
1. Select the specific access and permissions you want this application password to have.
    - Account: `read`
    - Team membership: `read`
    - Projects: `read`
    - Repositories: `read and write`
    - Pull requests: `read and write`
    - Webhooks: `read and write`

6. Copy the generated password and either record or paste it into the application you want to give access. __The password is only displayed this one time__.

This image shows the permissions screen in Bitbucket:

![Bitbucket API token](/images/bitbucket-api-token.png)


## Repository variables

Next, you will need [repository variables](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/#Repository-variables) at the
repository level which will later be [referenced in your pipeline](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/).

These will consist of the following:

1. Amazon EKS name of your cluster: `AWS_EKS_CLUSTER`
1. Snyk API token for authenticating with your Snyk account: `SNYK_TOKEN`
1. AWS Identity & Access Management User [key and secret](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for secure authenticated interactions with the AWS API: `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`
1. AWS region you will be deploying to: `AWS_DEFAULT_REGION`
1. Amazon ECR [URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html) for your repository: `AWS_ECR_URI`
1. Container image name: `IMAGE`

This screenshot shows those repository variables:
![Repository Variables](/images/bitbucket-repo-vars.png)


{{% notice tip %}}
It is recommended that you use [Snyk Service accounts](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts) and [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) when creating accounts.
{{% /notice %}}
