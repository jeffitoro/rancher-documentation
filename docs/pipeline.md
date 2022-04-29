---
layout: default
title: Pipelines
nav_order: 5
---

# Pipelines
Add your pipelines with github.

---

### Configure pipeline
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/configure-pipelines.png" />](/assets/images/pipelines/configure-pipelines.png)

### Authorize pipeline
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/authorize-pipelines.png" />](/assets/images/pipelines/authorize-pipelines.png)

### Authorize with your token github pipeline
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/token-auth-pipelines.png" />](/assets/images/pipelines/token-auth-pipelines.png)

### In github, in your project authorize connection with rancher
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/githup-oauth-pipelines.png" />](/assets/images/pipelines/githup-oauth-pipelines.png)
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/register-oauth-pipelines.png" />](/assets/images/pipelines/register-oauth-pipelines.png)

### Put your credential given
Put in rancher your clientId et clientSecret

### You have access to yor compte GitHub
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/repositories-pipelines.png" />](/assets/images/pipelines/repositories-pipelines.png)

### Your project structure have to be
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/pipelines/structure-deploy-pipelines.png" />](/assets/images/pipelines/structure-deploy-pipelines.png)

## Codes in your project for deploy
### Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: laravel
  labels:
    app: laravel
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      imagePullSecrets:
        - name: pipeline-docker-registry
      containers:
        - name: web
          image: ${CICD_IMAGE}:${CICD_EXECUTION_SEQUENCE}
          ports:
            - containerPort: 80
            - containerPort: 6001
              name: websocket-port
```
### Pipeline
```yaml
stages:
- name: Publish image laravel
  steps:
  - publishImageConfig:
      dockerfilePath: ./.docker/php/Dockerfile.prod
      buildContext: .
      tag: web:${CICD_EXECUTION_SEQUENCE}
- name: Deploy
  steps:
  - applyYamlConfig:
      path: ./.deploy/deployment_php.yml
branch:
  include:
  - production
  exclude:
  - branch
notification: {}
```