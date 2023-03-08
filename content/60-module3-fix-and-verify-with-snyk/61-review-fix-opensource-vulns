---
title: "Review and Fix Open Source Vulnerabilities in Snyk"
chapter: true
weight: 61
---

# Overview
We'll start by reviewing the Open Source vulnerabilities in the Goof application. Now that you've connected your Bitbucket Repo and ECR into Snyk, you can review the findings directly within the Snyk UI. 

### Step 1 - Review Snyk Open Source results
Let's start by reviewing the vulnerabilities introduced into the Container from the Open Source Libraries used by the Goof application. Click into the package.json under the Bitbucket Import.

The default Issues view shows an Issue Card for each Vulnerability. In the Snyk UI, issues are organized by Snyk's Priority Score, which considers factors such as availability of a fix, exploitability, and others to help you focus on the most important issues. Hover over each Issue's Priority Score to show what factors influenced the score for that issue.

### Step 2 - Filter Snyk Open Source results
From this view, the filters on the left help to narrow down the most urgent issues to fix. Apply the filters for "Critical" Severity, "Mature" Exploit Maturity, and "Fixable" Fixability to focus your attention on Exploitable, Fixable, Critical Severity Issues to start. 

These capabilities are intended to help teams reduce the issue backlog to the most Critical Issues that are actionable. They can help teams focus initial remediation efforts and build momentum around fixing. 

### Step 3 - Remediate an Open Source Issue
You might have noticed that in the Bitbucket Import Project, each Issue Card has a "Fix this Vulnerability" button. This allows you to Open a Pull Request directly from Snyk with the proposed fix for the vulnerability. Click the "Fix this Vulnerability" button for the Zip Slip vulnerability in adm-zip.

In the next page,  confirm the PR by clicking "Open a Fix PR". 

Once the PR is open, you'll be directed to Bitbucket to review. Notice the extra information provided in the body of the PR, which includes the Priority Score, Severity, Exploit Maturity, and links to more information.

After reviewing the code changes at the bottom of the PR, select "Merge" to merge this into your Repo.

### Step 4 - Verify the Fix
Once Merged, your Bitbucket Pipeline will run to re-build and push the Container Image. This will take a few minutes. When the Snyk tests run, the Pipeline Execution output will no longer show the Zip Slip vulnerability in adm-zip 0.4.7.

You can verify this fix by navigating back to Snyk and re-testing the Bitbucket project.

You can also verify this fix in Cloud9 by pulling the repo and running `snyk test`. 

```sh
git pull
snyk test
```

Once the Container is pushed to ECR, import the newly built container image tag like you did before to see a reduction in vulnerabilites in the ECR-imported project.

Next we'll demonstrate how to fix issues in the Container Base Image.
