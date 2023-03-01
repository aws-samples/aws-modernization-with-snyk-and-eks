---
title: "Create a Bucket Password"
chapter: true
weight: 41 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---


# Overview
In this section, we'll configure Snyk to have access to your Bitbucket environment.  This requires you to create a Personal Access Token on Bitbucket which we'll use in Snyk for your workspace

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


