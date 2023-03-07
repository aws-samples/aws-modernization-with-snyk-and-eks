---
title: "(Optional) Provision an Amazon EKS cluster"
chapter: true
weight: 40
---

# Introduction

In this section, we describe how to create an EKS cluster.  This step is optional during live workshops due to the time required to wait for the creation of the asset.

## Install eksctl

You'll need to install the `eksctl` command line tool to your Cloud9 environment.  From a terminal in Cloud9, enter these commands to download and install the binary:

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

```
sudo mv /tmp/eksctl /usr/local/bin
```

This should get you the binary where the following command should show how many EKS clusters you have in your environment.  At the start of the workshop, you will have no clusters.

```
eksctl get cluster
```

## Install kubectl

You'll need to install `kubectl` command line tool to your Cloud9 environment.  From a terminal in Cloud9, enter these commands to download and install the binary:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

```
chmod +x ./kubectl
```

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

```
kubectl version --output=yaml
```


## CLI Invocation

One easy way to setup an EKS cluster is to run the command as shown below in your Cloud9 environment.  You need two pieces of information:

- The name of your cluster identified as `NAME_OF_YOUR_CLUSTER` below.  Any name works, and we recommend `aws-workshop` as an example.
- The name of your keypair identified as `NAME_OF_YOUR_KEYPAIR` below.  This is the keypair you defined earlier.

```
eksctl create cluster --name NAME_OF_YOUR_CLUSTER \
--region us-east-1 \
--zones=us-east-1a,us-east-1b,us-east-1c \
--ssh-access \
--ssh-public-key NAME_OF_YOUR_KEYPAIR \
--managed \
--spot \
--instance-types=t3.small,t3.medium,t3.large,t2.medium,t2.small \
--tags "created-by=Marco Morales, created-on=2023-0301, Demo=workshop, owner=Marco Morales" \
--with-oidc
```

We recommend you paste the command to an editor and modify the contents there and then paste into your CLI.


This command takes between 20-40 minutes to run, so it is optional for most live workshops.  You do NOT have to specify the `--spot` parameter to utilize spot instances, but we do so in the interest of showing you can to save on costs.  

When the operation is complete, you will have an EKS cluster you can reference in your bitbucket variables.
