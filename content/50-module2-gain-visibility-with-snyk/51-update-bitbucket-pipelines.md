---
title: "Update Bitbucket Pipeline"
chapter: true
weight: 51
---

# Overview
We'll start by adding Snyk Scans to your pipeline.  This will require a few changes to the pipeline definition.

### Step 1 - Add Snyk scanning of open source
In the file `bitbucket-pipelines.yml` there is a block of pipeline definition within the `scan-app` stage.  Uncomment that block to enable Snyk Scans of open Source.

```yaml
scan-app: &scan-app
  - step:
      name: "Scan open source dependencies"
      caches:
        - node
      script:
        - echo "Scan open source Dependencies"
# Uncomment this block to enable Snyk Scan of open-source.
#        - pipe: snyk/snyk-scan:0.5.3
#          variables:
#            SNYK_TOKEN: $SNYK_TOKEN
#            LANGUAGE: "npm"
#            PROJECT_FOLDER: "app/goof"
#            TARGET_FILE: "package.json"
#            CODE_INSIGHTS_RESULTS: "true"
#            SEVERITY_THRESHOLD: "high"
#            DONT_BREAK_BUILD: "true"
#            MONITOR: "false"
```

### Step 2 - Add Snyk scanning of open source

Next, uncomment the section to scan Docker files

```
scan-push-image: &scan-push-image
  - step:
      name: "Scan and push container image"
      services:
        - docker
      script:
        - docker build -t $IMAGE ./app/goof/
        - docker tag $IMAGE $IMAGE:${BITBUCKET_COMMIT}
# Uncomment this block to enable Snyk Scan of container images.
#        - pipe: snyk/snyk-scan:0.5.3
#          variables:
#            SNYK_TOKEN: $SNYK_TOKEN
#            LANGUAGE: "docker"
#            IMAGE_NAME: $IMAGE
#            PROJECT_FOLDER: "app/goof"
#            TARGET_FILE: "Dockerfile"
#            CODE_INSIGHTS_RESULTS: "true"
#            SEVERITY_THRESHOLD: "high"
#            DONT_BREAK_BUILD: "true"
#            MONITOR: "false"
        - pipe: atlassian/aws-ecr-push-image:2.0.0
...
```