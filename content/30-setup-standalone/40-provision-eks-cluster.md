---
title: "(Optional) Provision an Amazon EKS cluster"
chapter: true
weight: 40
---

# Introduction

In this section, we describe how to create an EKS cluster.  Setting up an EKS cluster is a neat exercise and worth reviewing at a high level in guided workshops, and you doing them in a standalone workshop.

This step is optional during live workshops due to the time required to wait for the creation of the asset.  

You will need a few things to provision the cluster.  Some are covered in other sections of this workshop:

**Prerequisites**
- You have to create an AWS user, plus AWS keys.  This user will deploy your container to your cluster from your pipeline.
- Ensure you have a keypair available to you
- Attach a new IAM role for Cloud9 for permissions
- Disable AWS managed temporary credentials in Cloud9

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

You'll need to install `kubectl` command line tool to your Cloud9 environment.  From a terminal in Cloud9, enter these commands to download and install the binary.  We separate the commands one-at-a-time to ensure they work for you.

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

## Modify your kubectl configuration

Once your envionrment is up and running, you have to adjust your ConfigMap to permit the user you create access to your EKS cluster.

This is necessary in Event Engine settings because of how we are actually running under an assumed role as shown by this command:

```bash
TeamRole:~/environment/workshop-patterns-library-atlassian-aws (master) $ aws sts get-caller-identity
{
    "UserId": "AROASJIRQPIJZH2IKKL25:i-055b75e64b72627bd",
    "Account": "157339908627",
    "Arn": "arn:aws:sts::157339908627:assumed-role/workshop-cloud9/i-055b75e64b72627bd"
}
```

See how that is an assumed role?  One good option is to work with the new user you created.

Assuming your user has a name like, `marco`, we'll show you what to do next.

In Cloud9, run this command to bring up a VI editor:

```bash
kubectl edit -n kube-system configmap/aws-auth
```

You'll see a file with entries like `mapAccounts` and `mapRoles`.  You'll have to add an entry for `mapUsers` as shown below:

```yaml
apiVersion: v1
data:
  mapAccounts: |
    - "157339908627"
  mapRoles: |
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::157339908627:role/eksctl-marco-eks-cluster2-nodegro-NodeInstanceRole-AH77RPOZ3I7C
      username: system:node:{{EC2PrivateDNSName}}
  mapUsers: |
    - userarn: arn:aws:iam::157339908627:user/marco
      username: marco
      groups:
        - system:masters
kind: ConfigMap
```

The new blocks are:

```yaml
  mapAccounts: |
    - "157339908627"
```

and

```yaml
  mapUsers: |
    - userarn: arn:aws:iam::157339908627:user/marco
      username: marco
      groups:
        - system:masters
```
where you may be able to see the ARN is for your user, and the account we're mapping to is embedded in that ARN.  This account number is specific to your Event Engine workshp day.


When you save this file with the vi `Escape - Colon - w - q` sequence, you should see this message:

```
configmap/aws-auth edited
```

Next, let's bind your user to the `cluster-admin` role for the cluster.  With only one cluster we're in good shape to rely on our new EKS cluster as the default, so we don't need to specify it.  The binding name is semi-arbitrary, and we name is something clear, `marco-admin-binding` in the example below.  Copy this command and edit in your name and run it:

```
kubectl create clusterrolebinding YOURUSER-admin-binding --clusterrole=cluster-admin --user=YOURUSER
```

In our workshop example, we see this:

```
kubectl create clusterrolebinding marco-admin-binding --clusterrole=cluster-admin --user=marco
clusterrolebinding.rbac.authorization.k8s.io/marco-admin-binding created
```

These command will let you deploy your container to your kubernetes cluster via user + AWS keys in a pipeline.  That is great for replicating a working pipeline.

