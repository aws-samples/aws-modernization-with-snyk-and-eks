---
title: "Enable Bitbucket Repository Scanning"
chapter: true
weight: 54
---

# Overview
In this section, we'll add your Bitbucket repository to Snyk in the same style as we added your Amazon ECR to Snyk.  This gives your entire team visibility into the status of your repository.

## Step 1: Enable the Bitbucket Cloud integration

Navigate to your Snyk organization and find the Bitbucket Cloud integration.  In the image below, we filtered the integration list for `bitbucket` to find the Bitbucket Cloud App

![Snyk Bitbucket Cloud integration](../images/snyk-atlassian-integration.png)

Clicking into the integration presents you with a screen to connect your repository.

![Snyk Bitbucket Cloud grant access](../images/snyk-atlassian-integration-grant-access.png)

You'll be asked a few questions about permissions and granting access.  When the process is complete, you'll have the option of configuring the integration.  For the purpose of this workshop, we'll start with defaults, and review few options to enable more functionality.

## Step 2: Add your repositories

Next, click on the button entitled, `Add your Bitbucket Cloud App entities to Snyk` to import your repositories from Bitbucket.  Snyk supports popular Git providers, and we focus on Bitbucket in this workshop.  

![Snyk Bitbucket Cloud success](../images/snyk-atlassian-integration-success.png)

In the example below, we are adding the workshop repository given the name `plaa-1` as shown below.

![Snyk Bitbucket Cloud import](../images/snyk-atlassian-integration-import-repositories.png)

After a few moments, the import should be complete.  The result is all of the projects within the repository are made visible to all of the users in your team.

_Note: You may seen an error on the import of the `bitbucket_pipelines.yml` file.  Snyk tries to analyze different types of files, including YAML, but does not process Bitbucket Pipeline definitions.  You may safely ignore this error._

![Snyk Bitbucket Cloud projects](../images/snyk-atlassian-integration-projects.png)
