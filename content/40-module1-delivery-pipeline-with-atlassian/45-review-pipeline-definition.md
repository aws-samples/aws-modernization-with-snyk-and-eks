---
title: "Review Bitbucket Pipeline"
chapter: true
weight: 45 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

# Overview
In this section, we review the bitbucket pipeline and run it to deploy to ECR.  The repository contains an already defined pipeline, tailored to run with your details per the repository variables you configured.

### Step 1 - Review the pipeline definition

Navigate to the repository view for the file `bitbucket-pipelines.yml` and review the contents below.  The entire pipeline defintion is provided here for you to review with the instructor to review the following:

- The overall structure
- The build step
- The push step
- The use of the embedded Snyk Scan, presently commented out


```yaml
image: atlassian/default-image:2


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
      artifacts:
        - app/**

scan-app: &scan-app
  - step:
      name: "Scan open source dependencies"
      caches:
        - node
      script:
        - echo "Scan open source Dependencies"
        # Uncomment the following lines to enable Snyk Open Source Scanning
        # - pipe: snyk/snyk-scan:0.5.3
        #   variables:
        #     SNYK_TOKEN: $SNYK_TOKEN
        #     LANGUAGE: "npm"
        #     PROJECT_FOLDER: "app/goof"
        #     TARGET_FILE: "package.json"
        #     CODE_INSIGHTS_RESULTS: "true"
        #     SEVERITY_THRESHOLD: "high"
        #     DONT_BREAK_BUILD: "true"
        #     MONITOR: "false"

        - pipe: snyk/snyk-scan:0.5.3
          variables:
            SNYK_TOKEN: $SNYK_TOKEN
            SNYK_TEST_JSON_INPUT: "snyk-test-output.json"


scan-push-image: &scan-push-image
  - step:
      name: "Scan and push container image"
      services:
        - docker
      script:
        - docker build -t $IMAGE ./app/goof/
        - docker tag $IMAGE $IMAGE:${BITBUCKET_COMMIT}
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
        - pipe: atlassian/aws-ecr-push-image:2.0.0
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            IMAGE_NAME: $IMAGE
            TAGS: '${BITBUCKET_COMMIT}'

deploy-app: &deploy-app
  - step:
      name: "Deploy application"
      deployment: staging
      script:
        - pipe: atlassian/aws-eks-kubectl-run:2.2.0
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            CLUSTER_NAME: '$AWS_EKS_CLUSTER'
            KUBECTL_COMMAND: 'apply'
            RESOURCE_PATH: "./deployment/goof-service.yaml"
        - envsubst < ./deployment/goof-deployment-template.yaml > ./deployment/goof-deployment.yaml
        - cat ./deployment/goof-deployment.yaml
        - pipe: atlassian/aws-eks-kubectl-run:2.2.0
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            CLUSTER_NAME: '$AWS_EKS_CLUSTER'
            KUBECTL_COMMAND: 'apply'
            RESOURCE_PATH: './deployment/goof-deployment.yaml'

pipelines:
  default:
    - <<: *test-app
    # Uncomment this line to enable the scanning of the application.
    # - <<: *scan-app
    - <<: *scan-push-image
    # Uncomment this line to enable the deployment to EKS
    # - <<: *deploy-app
```

Once you review, let's now run the pipeline.

### Step 2 - Run the pipeline

Once the environment variables are setup, the pipeline is designed to run "as-is."

In Bitbucket, navigate to your repository and enable pipelines.  On free accounts, you usually have an allotment of minutes to perform the activity, and that allotment is well within the scope of this workshop.  You may need to enable the pipeline.

![Enable Pipeline](/images/bitbucket-pipeline-enable.png)

Once enabled, you can run the pipeline by accepting the default branch `master` and the default pipeline name `default`


![Run Pipeline](/images/bitbucket-run-pipeline.png)


In the next module, we'll add Snyk scanning and review the results.
