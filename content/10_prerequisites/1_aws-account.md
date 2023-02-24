+++
title = "AWS Account"
chapter = false
weight = 1
+++

{{% notice note %}}
This section is for people running on their own infrastructure.  If you are running as part of an AWS Event Engine event, you can skip this page.
{{% /notice %}}

{{% notice warning %}}
If you choose to run this workshop on your account, and not part of a hosted workshop, __you are responsible__ for the cost of the AWS services used while running this workshop in your AWS account.
Your account __must__ have the ability to create new IAM roles and scope other IAM permissions.
{{% /notice %}}

{{% notice note %}}
If you already have an AWS account, and have IAM Administrator access, go to the
[Provision AWS services]({{< ref "#provision-aws-services" >}}) section.
{{% /notice %}}



## Create an account 

### Step 1
If you don't already have an AWS account with Administrator access: [create
one now](http://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html#sign-up-for-aws)

### Step 2
Once you have an AWS account, ensure you are following the remaining workshop steps
as an **IAM user** with administrator access to the AWS account:
[Create a new IAM user to use for the workshop](https://console.aws.amazon.com/iam/home?region=us-east-1#/users$new)

### Step 3
Enter the user details:
![Create User](../images/iam-1-create-user.png)

### Step 4
Attach the AdministratorAccess IAM Policy:
![Attach Policy](../images/iam-2-attach-policy.png)

### Step 5
Click to create the new user:
![Confirm User](../images/iam-3-create-user.png)

### Step 6
Take note of the login URL and save:
![Login URL](../images/iam-4-save-url.png)

## Provision AWS services
We have simplified and automated the process for provisioning the necessary AWS services needed for this workshop.
This is possible through the [Snyk controller for Amazon EKS Quickstart](https://aws.amazon.com/solutions/partners/eks-snyk/). 

By clicking on the __Launch Stack__ button below, you will be redirected to the AWS CloudFormation console where you will
be prompted to complete the following steps:

- Create stack, click **Next**
- Specify stack details, click **Next**
- Configure stack options, click **Next**
- Scroll to bottom section under **Capabilities** and check both boxes and click **Create stack** 

When you are ready, click on the launch stack link below!

[Launch Stack on us-east-1](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template?stackName=Amazon-EKS-with-Snyk&templateURL=https://aws-quickstart.s3.us-east-1.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master.template.yaml)


[Launch Stack on us-west-2](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=Amazon-EKS-with-Snyk&templateURL=https://aws-quickstart.s3.us-west-2.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master.template.yaml)

{{% notice info %}}
The installation of the Snyk Monitor on Kubernetes takes several minutes. Please continue to the next section.
{{% /notice %}}

## Proceed to Getting Started

Once you have completed the step above, you can leave the AWS console open. You can now move to the [**Getting Started**]({{< relref "20_guided" >}}) section.
