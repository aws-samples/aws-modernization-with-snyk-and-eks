+++
title = "Cleaning up"
chapter = true
weight = 80
+++

# Introduction

At the end of this workshop, you may wonder about cleanup.  For guided workshops running on an AWS Event Engine, your instances will be deleted when your event account is closed down.  Typically this is within a day.

For standalone executions, you should be aware of the ECR and EKS resources your created, plus any extra that may have arisen.

If you setup an EKS cluster via the CLI command we provided during this workshop, here is a command to undo the same cluster via a CloudFormation delete:

```bash
eksctl delete cluster --name NAME_OF_YOUR_CLUSTER --region us-east-1
```

This operation uses the implicit CloudFormation template to delete your resources.

You may also delete your ECR cluster through the console of via CLI.
