+++
title = "AWS Event Engine"
chapter = false
weight = 2
+++

{{% notice note %}} 
To complete this workshop, you are provided with an AWS account via the AWS Event Engine service. A 12-digit hash will be provided to you by event staff - this is your unique access code.  In the example below we use `123456789012`.
{{% /notice %}}



## Logging in

### Create AWS Account

#### Step 1

Connect to the portal by clicking the button or browsing to [https://dashboard.eventengine.run/](https://dashboard.eventengine.run/). 
The following screen shows up. Enter the provided hash in the text box. The button on the bottom right corner changes to
 **Accept Terms & Login**. Click on that button to continue.

![Event Engine](../images/event-engine-initial-screen.png)

#### Step 2

Choose **AWS Console**, then **Open AWS Console**.
Your workshop presenters will tell you when your account expires, and this is typically one day.  At expiration, all of your resources will be automatically deprovisioned. 

![Event Engine Dashboard](../images/event-engine-dashboard.png)

#### Step 4

Use a single region for the duration of this workshop. This workshop supports the following regions:

TODO : Confirm if we can also use us-east-1 and maybe one more.  I believe we should be able to use any region with EKS support

* us-west-2 (US West - Oregon)

Please select **US West (Oregon)** in the top right corner.

![Event Engine Region](../images/event-engine-region.png)

#### Step 5

We have simplified and automated the process for provisioning the necessary AWS services needed for this workshop.
This is possible through the [Snyk controller for Amazon EKS](https://github.com/aws-quickstart/quickstart-eks-snyk) AWS Quick Start. 
By clicking on the __Launch Stack__ button below, you will be redirected to the AWS CloudFormation console where you will
be prompted to complete the following steps:

- Create stack, **select appropriate AWS region** click **Next**
- Specify stack details, **input EKS cluster name & Snyk integration ID** click **Next**
- Configure stack options, click **Next**
- Scroll to bottom section under **Capabilities** and click **Create stack** 

When you are ready, click the button below!

[![Launch-Stack](../images/cloudformation-launch-stack.png)](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/create/template?stackName=Snyk-EKS&templateURL=https://aws-quickstart.s3.us-east-1.amazonaws.com/quickstart-amazon-eks/submodules/quickstart-eks-snyk/templates/eks-snyk.template.yaml)

## Proceed to Getting Started

Once you have completed the step above, you can leave the AWS console open. You can now move to the [**Getting Started**]({{< relref "20_guided" >}}) section. 