---
title: "Update Bitbucket Pipeline"
chapter: true
weight: 51
---

# Overview
We'll start by adding Snyk Scans to your pipeline for the code your teams write, the open source libraries they use, and the containers they build.  This will require a few changes to the pipeline definition.

You may make the changes directly in your Bitbucket Cloud UI, or via your editor with a `git push` in Cloud9.

### Step 1 - Add Snyk scanning of your code

We start by modifying the file `bitbucket-pipelines.yml` to enable the scan of your code.  Find the section below and uncomment as directed to enable the scanning of your custom code.

```yaml
test-app: &test-app
  - step:
      name: "Test application"
      caches:
        - node
      script:
        - cd app/goof
        - npm install
        # Uncomment the following lines to enable Snyk Scan of code
        # - curl https://static.snyk.io/cli/latest/snyk-linux -o snyk-linux
        # - chmod +x snyk-linux
        # - set -e
        # - EXIT_CODE=0
        # - ./snyk-linux -d code test || EXIT_CODE=$?
        # - echo $EXIT_CODE
```

### Step 2 - Add Snyk scanning of open source
Next, let's uncomment that block to enable Snyk Scans of open Source for the libraries your team uses.

```yaml
pipelines:
  default:
    - <<: *test-app
    # Uncomment this line to enable the scanning of the application.
    # - <<: *scan-app
    - <<: *scan-push-image
```

### Step 3 - Add Snyk scanning of open source

Finally, uncomment the section to scan dockerfile defintions.

```
scan-push-image: &scan-push-image
  - step:
      name: "Scan and push container image"
      services:
        - docker
      script:
        - docker build -t $IMAGE ./app/goof/
        - docker tag $IMAGE $IMAGE:${BITBUCKET_COMMIT}
        - echo "Scan Container images"
      # Uncomment this block to enable Snyk Scan of container images.
      #  - pipe: snyk/snyk-scan:0.5.3
      #    variables:
      #      SNYK_TOKEN: $SNYK_TOKEN
      #      LANGUAGE: "docker"
      #      IMAGE_NAME: $IMAGE
      #      PROJECT_FOLDER: "app/goof"
      #      TARGET_FILE: "Dockerfile"
      #      CODE_INSIGHTS_RESULTS: "true"
      #      SEVERITY_THRESHOLD: "high"
      #      DONT_BREAK_BUILD: "true"
      #      MONITOR: "false"
...
```


## Step 4: Commit and build

Commit your changes to trigger a pipeline build.  In the next section we'll review the results.
