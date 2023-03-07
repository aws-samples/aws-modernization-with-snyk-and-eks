---
title: "Setup Bitbucket CLI credentials"
chapter: true
weight: 55
---

# Setup Instructions
In this section, we'll summarize the instructions on how you can connect to Atlassian Bitbucket Cloud from the CLI in Cloud9.  This information is taken from the [Atlassian documentation for Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).

We will use this repository access in a later module

You have the option of using SSH keys, or an access token.  In normal situations you would use SSH keys.  For the purpose of this workshop, we'll use an access token in the spirit of username/password authentication.


## Setting up the Repository Access Token

Navigate to your forked Bitbucket repository and click on the repository settings.

![repository-settings](/images/atlassian-bitbucket-repository-settings.png)

In the security subsection, click on the Access Tokens heading, and the **Create Repository Access Token** button.

![repository-settings](/images/atlassian-bitbucket-repository-access-tokens.png)

Name the token `workshop-token` and grant **Repositories Write** permissions.  For this workshop, we only need to clone and commit, and we won't use the token for other operations.

![repository-settings](/images/atlassian-bitbucket-repository-token.png)


Click on create and save the token to a safe location for ths workshop.

You will only have one time to save this information, and you will need the commands to clone and push, which will look like this:

```
git clone https://x-token-auth:REALLYLONGNUMBER@bitbucket.org/marco-morales-snyk/workshop-patterns-library-atlassian-aws.git
```

```
git config user.email SOMENUMBER@bots.bitbucket.org
```
