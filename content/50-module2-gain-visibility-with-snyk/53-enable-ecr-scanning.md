---
title: "Enable ECR scanning"
chapter: true
weight: 53
---

# Overview
In this section, we'll describe how you can enable the scanning of Amazon ECR images from Snyk. This information is presented in the Snyk UI and is [documented at Snyk](https://docs.snyk.io/scan-containers/image-scanning-library/ecr-image-scanning).  We'll review the process in the context of the workshop to better illustrate the example.

{{% notice tip %}}
Snyk's integration for Amazon Elastic Container Registry (ECR) is enabled between one Amazon ECR registry and one Snyk organization. To 
integrate with multiple registries, create a unique Snyk organization for each registry.
{{% /notice %}}


## Obtain your Snyk Organization ID

From the Snyk console, navigate to __Settings__ and under the __General__ menu `Copy` your __Organization ID__.

![Snyk Organization ID](../images/snyk-api-token.png)

## Step 1: Enable the integration

For the purpose of this workshop, we will configure the integration manually to explain the different steps in the context of the workshop.  This also means we are creating brand-new resources and not adding to existing ones.  We'll use the documentation on the integrations page as the primary source of instructions, and supplement it here with editorial to better set the context.

Your instructor will also provide additional context and explanation.


Start by navigating to Snyk and your organization's Integrations page.   Here we show a filtered view for "ecr".

![Snyk ECR Integration](../images/aws-ecr-integration.png)

Clicking into the tile takes you to a page with two fields to fill in, and instructions on what to do.

The first field is your region, and we'll assume `us-east-1`
The second field is the AWS IAM Role ARN we'll create in this page, which will have the assumed name of the form  `arn:aws:iam::YOURACCOUNTNUMBER:role/SnykServiceRole`.  Let's create that IAM Role.

## Step 2: Create a new IAM Policy

Navigate to the AWS Console for the **IAM service**, and then **Policies**.  We will `Create policy` with the suggested name `AmazonEC2ContainerRegistryReadOnlyForSnyk` and have the body defined as:

```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "SnykAllowPull",
   "Effect": "Allow",
   "Action": [
    "ecr:GetLifecyclePolicyPreview",
    "ecr:GetDownloadUrlForLayer",
    "ecr:BatchGetImage",
    "ecr:DescribeImages",
    "ecr:GetAuthorizationToken",
    "ecr:DescribeRepositories",
    "ecr:ListTagsForResource",
    "ecr:ListImages",
    "ecr:BatchCheckLayerAvailability",
    "ecr:GetRepositoryPolicy",
    "ecr:GetLifecyclePolicy"
   ],
   "Resource": "*"
  }
 ]
}
```

## Step 3: Create a new IAM Role

Navigate to the AWS Console for the **IAM service**, and then **Roles**.  We will `Create role` with the suggested name `SnykServiceRole`.  This role is for the AWS EC2 service, and the role utilizes the policy we just created.

## Step 4: Harden the usability scope

The integration works when you specify your Snyk organization by ID.

For the purpose of this workshop, you are expected to only have one entry, and the format of the text will be like this:

```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Principal": {
    "AWS":  "arn:aws:iam::198361731867:user/ecr-integration-user"
   },
   "Action": "sts:AssumeRole",
   "Condition": {
    "StringEquals": {
     "sts:ExternalId": "2530db28-bf52-489f-be17-c313c0bed5b7"
    }
   }
  }
 ]
}
```

As your teams add more organizations, you will need to specify the `sts:ExternalId` parameter differently, as shown below:

```json
"StringEquals": {
                    "sts:ExternalId": [
                        "3a4d6c3d-cf74-4d52-bda7-39915ea5c853",
                        "c29dd000-ee52-438a-a5af-e773523506f4"
                    ]
                }
```

Notice how the value shifts to an array format from before.


## Step 5: Use the Role ARN

Once you are finished with creating the hardened IAM Role that uses the IAM Policy, you will have access to the ARN for the role.  Copy that value to the Snyk UI and save your configuration.

You'll see a banner announcing the integration is successful.
![Snyk ECR Success](../images/aws-ecr-integration-success.png)


## Step 6: Add ECR images to Snyk

Click on the button to add your ECR images to Snyk to enable their scanning withing Snyk.

![Snyk Add Images](../images/aws-ecr-add-images.png)

Within a few moments, your images will be imported as projects and we can review the results.  This view is especially helpful when working across a team, given the shared visibility into the images.  You will see entries for both the image, as well as the embedded open-source package.  This is handy for seeing both in the same context.

![Snyk ECR projects](../images/aws-ecr-snyk-projects.png)

Your instructor will walk you though the contents with some explanations.  Later, you will see how to remediate vulnerabilities.

