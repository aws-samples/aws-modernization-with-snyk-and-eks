---
title: "Scan files locally"
chapter: true
weight: 55
---

# Overview
In this section, we'll scan files with the Snyk CLI.  In this example, we'll use Snyk to get results in different ways to highlight the possibibilities.


## Step 1 - Clone your fork locally

Next, clone your forked repository into your Cloud9 environment. Please review Atlassian's documentation on 
how to [clone a repository](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html) for detailed 
instructions.

Open a terminal in your Cloud9 environment, and enter the following commands to navigate to your base directory and clone the forked repository vis HTTPS

```shell
cd ~/environment
git clone https://marco-morales-snyk@bitbucket.org/marco-morales-snyk/patterns-library-atlassian-aws.git
cd patterns-library-atlassian-aws
```

or this command to clone via SSH:

```shell
cd ~/environment
git clone git@bitbucket.org:marco-morales-snyk/patterns-library-atlassian-aws.git
cd patterns-library-atlassian-aws
```

This clones the environment to your local workspace.

## Step 2: Snyk for your custom code

Navigate to your Cloud9 environment and enter the following command to get you into the base directory:

```shell
cd ~/environment
cd patterns-library-atlassian-aws
ls -l app/goof
```

The output will look similar to the following:

```shell
$ ls -l app/goof
total 356
-rw-r--r-- 1 marco marco   2155 Mar  1 08:22 app.js
-rw-r--r-- 1 marco marco    575 Mar  1 08:22 app.json
-rw-r--r-- 1 marco marco   1402 Mar  1 08:22 db.js
-rw-r--r-- 1 marco marco    913 Mar  1 08:22 deploy-heroku.md
-rw-r--r-- 1 marco marco    314 Mar  1 08:22 docker-compose.yml
-rw-r--r-- 1 marco marco    203 Mar  1 08:22 Dockerfile
drwxr-xr-x 3 marco marco   4096 Mar  1 08:22 exploits
-rw-r--r-- 1 marco marco  11357 Mar  1 08:22 LICENSE
-rw-r--r-- 1 marco marco   1315 Mar  1 08:22 package.json
-rw-r--r-- 1 marco marco 292415 Mar  1 08:22 package-lock.json
drwxr-xr-x 5 marco marco   4096 Mar  1 08:22 public
-rw-r--r-- 1 marco marco   3398 Mar  1 08:22 README.md
drwxr-xr-x 2 marco marco   4096 Mar  1 08:22 routes
-rw-r--r-- 1 marco marco    641 Mar  1 08:22 utils.js
drwxr-xr-x 2 marco marco   4096 Mar  1 08:22 views
```

In this example, our deliberately vulnerable application is named goof, and the code is a node.js example.

If we look at the contents of the file at `app/goof/package.json` you will see a manifest for the project.  This includes the language specification for `node 6.14.1` and dependencies that include entries such as `adm-zip : 0.4.7`

This layout is typical and it is customary for developers to work through a CLI in their IDE or in a terminal window.

Let's start a Snyk scan of your code with the command you may recognize from the pipeline example:

```shell
$ snyk code test

Testing /home/marco/code/atlassian/workshop/plaa-1 ...

 ✗ [Medium] Cleartext Transmission of Sensitive Information
   Path: app/goof/app.js, line 72
   Info: http.createServer uses HTTP which is an insecure protocol and should not be used in code due to cleartext transmission of information. Data in cleartext in a communication channel can be sniffed by unauthorized actors. Consider using the https module instead.

 ✗ [Medium] Use of Hardcoded Credentials
   Path: app/goof/db.js, line 52
   Info: Do not hardcode passwords in code. Found hardcoded password used in password.

 ✗ [Medium] Information Exposure
   Path: app/goof/app.js, line 26
   Info: Disable X-Powered-By header for your Express app (consider using Helmet middleware), because it exposes information about the used framework to potential attackers.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
   Path: app/goof/routes/index.js, line 77
   Info: This endpoint handler performs a system command execution and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
   Path: app/goof/routes/index.js, line 166
   Info: This endpoint handler performs a file system operation and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
   Path: app/goof/routes/index.js, line 222
   Info: This endpoint handler performs a file system operation and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Cross-Site Request Forgery (CSRF)
   Path: app/goof/app.js, line 26
   Info: CSRF protection is disabled for your Express app. This allows the attackers to execute requests on a user's behalf.

 ✗ [High] Hardcoded Secret
   Path: app/goof/app.js, line 69
   Info: Avoid hardcoding values that are meant to be secret. Found a hardcoded string used in here.

 ✗ [High] NoSQL Injection
   Path: app/goof/routes/index.js, line 39
   Info: Unsanitized input from the HTTP request body flows into find, where it is used in an NoSQL query. This may result in an NoSQL Injection vulnerability.

 ✗ [High] NoSQL Injection
   Path: app/goof/routes/index.js, line 116
   Info: Unsanitized input from an HTTP parameter flows into findById, where it is used in an NoSQL query. This may result in an NoSQL Injection vulnerability.

 ✗ [High] NoSQL Injection
   Path: app/goof/routes/index.js, line 144
   Info: Unsanitized input from an HTTP parameter flows into findById, where it is used in an NoSQL query. This may result in an NoSQL Injection vulnerability.


✔ Test completed

Organization:      80fb7716-41a2-4bc4-a8a4-c10a7fd737cc
Test type:         Static code analysis
Project path:      /home/marco/code/atlassian/workshop/plaa-1

Summary:

  11 Code issues found
  4 [High]   7 [Medium]
  ```


Here, we see the same details in our pipeline and the website.  You can adjust the output to only list severities of type `high`:

```shell
snyk code test --severity-threshold=high
```

or with json output:
```shell
snyk code test --severity-threshold=high --json
```

See the [Snyk docs](https://docs.snyk.io/scan-application-code/snyk-code/cli-for-snyk-code) for more information

## Step 3: Snyk for your open source

Next, let's look at the results of your open-source vulnerabilties with similar commannds.  Snyk open-source supports a variety of languages, and some of the subcommands are specific to a language or framework.  We'll explore some common examples, starting with a straight scan of your open source:

```shell
 snyk test app/goof/

Testing app/goof/...

Tested 471 dependencies for known issues, found 93 issues, 379 vulnerable paths.


Issues to fix by upgrading:

  Upgrade adm-zip@0.4.7 to adm-zip@0.5.2 to fix
  ✗ Directory Traversal [High Severity][https://security.snyk.io/vuln/SNYK-JS-ADMZIP-1065796] in adm-zip@0.4.7
    introduced by adm-zip@0.4.7
  ✗ Arbitrary File Write via Archive Extraction (Zip Slip) [Critical Severity][https://security.snyk.io/vuln/npm:adm-zip:20180415] in adm-zip@0.4.7
    introduced by adm-zip@0.4.7

... LINES DELETED ...
Patchable issues:

  Patch available for lodash@4.17.4
  ✗ Prototype Pollution [High Severity][https://security.snyk.io/vuln/SNYK-JS-LODASH-567746] in lodash@4.17.4
    introduced by lodash@4.17.4 and 9 other path(s)

  Patch available for ms@0.6.2
  ✗ Regular Expression Denial of Service (ReDoS) [Medium Severity][https://security.snyk.io/vuln/npm:ms:20151024] in ms@0.6.2
    introduced by humanize-ms@1.0.1 > ms@0.6.2

... LINES DELETED ...
Issues with no direct upgrade or patch:
  ✗ Prototype Pollution [High Severity][https://security.snyk.io/vuln/SNYK-JS-AJV-584908] in ajv@6.10.2
    introduced by tap@11.1.5 > coveralls@3.0.9 > request@2.88.0 > har-validator@5.1.3 > ajv@6.10.2
  This issue was fixed in versions: 6.12.3
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JS-DECODEURICOMPONENT-3149970] in decode-uri-component@0.2.0
    introduced by tap@11.1.5 > nyc@11.9.0 > micromatch@3.1.10 > snapdragon@0.8.2 > source-map-resolve@0.5.1 > decode-uri-component@0.2.0 and 9 other path(s)
  This issue was fixed in versions: 0.2.2
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JS-DICER-2311764] in dicer@0.3.0
    introduced by express-fileupload@0.0.5 > connect-busboy@0.0.2 > busboy@0.3.1 > dicer@0.3.0
  No upgrade or patch available
... LINES DELETED ...

License issues:

  ✗ GPL-2.0 license (new) [High Severity][https://snyk.io/vuln/snyk:lic:npm:goof:GPL-2.0] in goof@1.0.1

... LINES DELETED ...

Organization:      marco-goof
Package manager:   npm
Target file:       package-lock.json
Project name:      goof
Open source:       no
Project path:      app/goof/
Licenses:          enabled
```

As you may notice, there is a substantial amount of information for vulnerabilities you can upgrade, those can you patch, and those you can't patch or upgrade.

You have other options, too.  Some are to specify how deep you want to traverse your directories.  Another one is useful to show your dependency tree:

```shell
snyk test app/goof/ --print-deps
goof @ 1.0.1
   ├─ adm-zip @ 0.4.7
   ├─ body-parser @ 1.9.0
   │  ├─ bytes @ 1.0.0
   │  ├─ depd @ 1.0.1
   │  ├─ iconv-lite @ 0.4.4
   │  ├─ media-typer @ 0.3.0
   │  ├─ on-finished @ 2.1.0
   │  │  └─ ee-first @ 1.0.5
   │  ├─ qs @ 2.2.4
   │  ├─ raw-body @ 1.3.0
   │  │  ├─ bytes @ 1.0.0
   │  │  └─ iconv-lite @ 0.4.4
   │  └─ type-is @ 1.5.7
   │     ├─ media-typer @ 0.3.0
   │     └─ mime-types @ 2.0.14
   │        └─ mime-db @ 1.12.0
   ├─ cfenv @ 1.2.2
   │  ├─ js-yaml @ 3.13.1
   │  │  ├─ argparse @ 1.0.10
   │  │  │  └─ sprintf-js @ 1.0.3
   │  │  └─ esprima @ 4.0.1
   │  ├─ ports @ 1.1.0
   │  └─ underscore @ 1.9.1

... LINES DELETED ...

```
This view is handy to see your transitive dependencies.

## Step 4: Snyk for your container

Next, let's look at the scan results for your containers

```shell
$ snyk container test --file=app/goof/Dockerfile node:6-stretch
```

At the time of this workshop, there were over 1000 issues, so let's filter this down so it is easier to see.

```shell
$ snyk container test --file=app/goof/Dockerfile node:6-stretch --severity-threshold=critical

Testing node:6-stretch...

✗ Critical severity vulnerability found in shadow/passwd
  Description: Out-of-Bounds
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN9-SHADOW-306269
  Introduced through: meta-common-packages@meta, shadow/login@1:4.4-4.1
  From: meta-common-packages@meta > shadow/passwd@1:4.4-4.1
  From: shadow/login@1:4.4-4.1
  Image layer: Introduced by your base image (node:6-stretch)
  Fixed in: 1:4.4-4.1+deb9u1

✗ Critical severity vulnerability found in python3.5/libpython3.5-stdlib
  Description: Buffer Overflow
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN9-PYTHON35-1063181
  Introduced through: python3.5/libpython3.5-stdlib@3.5.3-1+deb9u1, python3-defaults/libpython3-stdlib@3.5.3-1, python3.5@3.5.3-1+deb9u1, python3.5/python3.5-minimal@3.5.3-1+deb9u1, python3-defaults/python3@3.5.3-1, python3.5/libpython3.5-minimal@3.5.3-1+deb9u1
  From: python3.5/libpython3.5-stdlib@3.5.3-1+deb9u1
  From: python3-defaults/libpython3-stdlib@3.5.3-1 > python3.5/libpython3.5-stdlib@3.5.3-1+deb9u1
  From: python3.5@3.5.3-1+deb9u1 > python3.5/libpython3.5-stdlib@3.5.3-1+deb9u1
  and 8 more...
  Image layer: Introduced by your base image (node:6-stretch)
  Fixed in: 3.5.3-1+deb9u4

... LINES DELETED ...
Organization:      marco-goof
Package manager:   deb
Target file:       app/goof/Dockerfile
Project name:      docker-image|node
Docker image:      node:6-stretch
Platform:          linux/amd64
Base image:        node:6-stretch
Licenses:          enabled

Tested 413 dependencies for known issues, found 56 issues.

Base Image      Vulnerabilities  Severity
node:6-stretch  1100             56 critical, 234 high, 251 medium, 559 low

Recommendations for base image upgrade:

Alternative image types
Base Image                  Vulnerabilities  Severity
node:14.21.3-bullseye-slim  43               0 critical, 0 high, 0 medium, 43 low
node:lts-bullseye-slim      44               0 critical, 1 high, 0 medium, 43 low
node:19.7-buster-slim       59               0 critical, 2 high, 1 medium, 56 low
node:19.7-buster            367              0 critical, 3 high, 8 medium, 356 low

Debian 9 is no longer supported by the Debian maintainers. Vulnerability detection may be affected by a lack of security updates.

Pro tip: use `--exclude-base-image-vulns` to exclude from display Docker base image vulnerabilities.

Snyk found some vulnerabilities in your image applications (Snyk searches for these vulnerabilities by default). See https://snyk.co/app-vulns for more information.

To remove these messages in the future, please run `snyk config set disableSuggestions=true`

Learn more: https://docs.snyk.io/products/snyk-container/getting-around-the-snyk-container-ui/base-image-detection
```

In this other example, we use `exclude-base-image-vulns` to limit output to only show the vulnerabilities introduced by the base image.  This is for those cases where your team wants to know the list of vulnerabilities introduced by your definitions.  In our example, we didn't introduce any, but we can see our base image has.

```shell
$ snyk container test --file=app/goof/Dockerfile node:6-stretch --exclude-base-image-vulns

Testing node:6-stretch...

Organization:      marco-goof
Package manager:   deb
Target file:       app/goof/Dockerfile
Project name:      docker-image|node
Docker image:      node:6-stretch
Platform:          linux/amd64
Base image:        node:6-stretch
Licenses:          enabled

✔ Tested 413 dependencies for known issues, no vulnerable paths found.

Base Image      Vulnerabilities  Severity
node:6-stretch  1100             56 critical, 234 high, 251 medium, 559 low

Recommendations for base image upgrade:

Alternative image types
Base Image                  Vulnerabilities  Severity
node:14.21.3-bullseye-slim  43               0 critical, 0 high, 0 medium, 43 low
node:lts-bullseye-slim      44               0 critical, 1 high, 0 medium, 43 low
node:19.7-buster-slim       59               0 critical, 2 high, 1 medium, 56 low
node:19.7-buster            367              0 critical, 3 high, 8 medium, 356 low

Debian 9 is no longer supported by the Debian maintainers. Vulnerability detection may be affected by a lack of security updates.
```



# Next steps

We omitted the use case for Snyk in popular IDEs.  This is an example covered in many other assets, and the general experience is you and your team can see the results of security scans in their favorite environments, including guidance and remediation.

Until now, you have been given information.  Sometimes teams start their application security journey by first seeing the results of scans, and trying to make sense of the information.  Our goal was to help set some context about _what_ you are seeing and _why_.  In the next section, we'll start to show you how you can make changes to address these vulnerability issues.
