---
title: "Forking the repository"
chapter: true
weight: 44 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

# Overview
In this section we fork the repository and clone it into your Cloud9 environment.

### Step 1 - Fork the repository

In Atlassian Bitbucket, click [here](https://bitbucket.org/snyk/patterns-library-atlassian-aws/fork) to fork the `upstream` repository into your Bitbucket 
account. For detailed instructions on how to [fork a respository](https://support.atlassian.com/bitbucket-cloud/docs/fork-a-repository/), 
please review Atlassian's documentation.

![Forking Repository](/images/atlassian-fork.png)

### Step 2 - Clone your fork locally

Next, clone your forked repository into your Cloud9 environment. Please review Atlassian's documentation on 
how to [clone a repository](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html) for detailed 
instructions.

Open a terminal in your Cloud9 environment, and enter the following commands to navigate to your base directory and clone the forked repository vis HTTPS

```shell
cd ~/environment
git clone https://marco-morales-snyk@bitbucket.org/marco-morales-snyk/patterns-library-atlassian-aws.git
cd patterns-library-atlassian-aws
```

or this command to clone via SSH:

```shell
cd ~/environment
git clone git@bitbucket.org:marco-morales-snyk/patterns-library-atlassian-aws.git
cd patterns-library-atlassian-aws
```

This clones the environment to your local workspace.
