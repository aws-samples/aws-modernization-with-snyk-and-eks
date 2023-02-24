+++
title = "Adding Kubernetes workloads"
chapter = false
weight = 3
+++

![K8s](../images/kubernetes-01.png)

## Background

In the Snyk Blog, ["From image security to workload security"](https://snyk.io/blog/from-image-security-to-workload-security/), we discuss the challenge of configuration
in Kubernetes, and the fact that while the Kubernetes API provides a powerful abstraction for building cloud native systems, it is
also insecure by default. This article also shares insight into some common configuration properties that are often overlooked:

Security Context | Description
---------------------|---------------------
CPU and Memory limits | Limiting the expected CPU and Memory limits has operational as well as security benefits. In the context of security, this is about limiting the impact potential denial of service attacks have in affecting the app, rather than the node, and potentially the whole cluster.
runAsNonRoot | By default, containers run as the root user. This property prevents that at the container runtime, meaning, if an attacker was able to execute a command in the context of the container, they would only have limited permissions.
readOnlyRootFilesystem | By default, the file system mounted for the container is writable. That means, an attacker who compromises the container can also write to disk, which makes certain attacks easier. If your containers are stateless, then you don’t need a writable filesystem.
Capabilities | Linux capabilities control, at a low-level, what processes do in the container—from writing to disk, to communicating over the network. Dropping all capabilities and adding in those that are required is possible, but requires understanding the list of capabilities.

The following exercises will demonstrate these insecure configurations and how to identify and fix them with Snyk.

### Enable pipelines

Let's get started by enabling pipelines in our repository. Let's go to our Bitbucket repository and select __Pipelines__ from the menu bar.
Scroll to the bottom and click the __Enable__ button to kick off a pipeline run.

![Bitbucket Pipeline Enabled](../images/bitbucket-pipelines-enable.png)

### Adding workloads

Now, let's go to our Snyk app. Let's navigate to __Integrations__ and select __Kubernetes__. Since we previously deployed the 
Snyk controller into our cluster, this should appear as __Connected to Kubernetes__ and we should be able to click the button to 
__Add your Kubernetes workloads to Snyk__.

![K8s enabled](../images/snyk-eks-integration-01.png)

Next, we will select our cluster and our __goof__ app. Click __Add selected workloads__ when ready.

![K8s selected](../images/snyk-eks-integration-02.png)

Once the scan is complete, you will see the following results:

![K8s results](../images/snyk-eks-integration-03.png)

The results, should not surprise us. If we examine the manifests and compare that against the best practices we previously referenced, 
not only are configurations overlooked, `securityContext` is entirely absent. Let's explore this in more detail in the next module.
