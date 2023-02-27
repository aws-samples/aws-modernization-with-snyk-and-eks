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


## Extra content to remove.
TODO: Figure out if we need this information

Enable the Snyk Open Source [integration](https://solutions.snyk.io/snyk-academy/open-source/create-source-control-integration) to Bitbucket and 
[import your SCM project](https://solutions.snyk.io/snyk-academy/open-source/import-scm-project). Understand transitive dependencies and how Snyk can generate automatic pull requests 
to streamline your process.

Enable Snyk Container [integration](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-) to 
Amazon Elastic Container Registry (ECR) and [import](https://solutions.snyk.io/snyk-academy/container/container-registry-and-image-import) your container images. Learn how
Snyk provides base image ugprade recommendations.

[Install the Snyk controller](https://support.snyk.io/hc/en-us/articles/360011128137-Install-the-Snyk-controller-on-Amazon-Elastic-Kubernetes-Service-Amazon-EKS-) on 
Amazon Elastic Kubernetes Service (Amazon EKS) and [add workloads for scanning](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning).
Understand test results, how to interpret Snyk's [Priority Score](https://support.snyk.io/hc/en-us/articles/360010906897-Snyk-Priority-Score-and-Kubernetes), and how to 
fix configuration issues.


In this module, you will go through guided exercises that demonstrate how to fix for vulnerabilities and insecure configurations. 
You will apply what you learned in the previous modules and apply fixes to your application, container image, and Kubernetes
configuration to secure your application.

