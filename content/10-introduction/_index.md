+++
title = "Introduction"
chapter = true
weight = 10
+++

# Learning Objectives

![Snyk Bitbucket Flow](images/snyk-bitbucket-flow.png)

The learning goals of this workshop include:

- Understand [Software Composition Analysis (SCA)](https://snyk.io/blog/what-is-software-composition-analysis-sca-and-does-my-company-need-it/) and its importance in your developer workflows.
- Discover vulnerabilities in your application open source dependencies.
- Implement Snyk's [container image](https://snyk.io/blog/detecting-vulnerabilities-in-container-images/) scanning in your [Continuous integration](https://aws.amazon.com/devops/continuous-integration/) and 
[Continuous delivery](https://aws.amazon.com/devops/continuous-delivery/) (CI/CD) pipeline.
- Leverage the [Snyk Pipe](https://bitbucket.org/product/features/pipelines/integrations?p=snyk/snyk-scan) for Bitbucket Pipelines to secure your application.
- [Fix insecure Kubernetes configuration at the source](https://snyk.io/blog/fix-insecure-kubernetes-configuration/).

## Intended Audience

- Developers
- Security/Application Teams
- DevOps/DevSecOps Engineers
- Cloud/Solutions Architects

# Content Structure

We have structured the various subjects covered in this workshop into specific modules. Each module will provide
context on the theory behind the techniques presented as well as hands-on examples.

## Module 1 - The Atlassian Delivery Pipeline

We'll fork a public repository and configure its Bitbucket Pipeline to deploy your container image to Amazon ECR.  

## Module 2 - Gain Visibility with Snyk

We'll integrate your repository and Amazon ECR into Snyk to gain visibility of your code, open-source dependencies, and containers.  

## Module 3 - Fix and Verify with Snyk

We'll propagate a fix and observe the results in Amazon ECR.  This entails opening a Fix PR for review in Bitbucket.


## Module 4 - Extra Credit

Introduce Snyk Monitor in your CI/CD pipeline. 
Introduce the Snyk Kubernetes integration.
Open-ended tests and experimentation
