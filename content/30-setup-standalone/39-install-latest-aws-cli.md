---
title: "Install latest AWS CLI"
chapter: true
weight: 39
---

# Introduction

In this section, we describe how you can update your latest AWS CLI to version 2.

## Install AWS CLI v2

The following is an abbreviated form of the [online instructions to update your AWS CLI to version 2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

In your Cloud9 environment, open a new terminal and run the following commands:

```shell
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

Once this operatio is complete, close your terminal and open a new one.  Then enter this command to verify you are at version 2:

```shell
aws --version
```
