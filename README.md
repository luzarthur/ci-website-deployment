# Continuous Integration Pipeline for Website Deployment

This repository contains the Continuous Integration (CI) pipeline configuration for deploying a website. The pipeline consists of several jobs organized into stages, each performing specific tasks related to testing, packaging, and deploying the website to various environments.

## Overview

The CI pipeline includes the following stages:

1. **Test**: Verifies the website for broken URLs and checks for vulnerabilities.
2. **Package**: Packages the website for deployment, caching the build artifacts.
3. **Deploy**: Deploys the website to different environments such as development, release, and production.

## Jobs

### Test Website
- **Purpose**: Verify the website for broken URLs using the Broken Link Checker tool.
- **Tools**: `broken-link-checker`, `wait-on`
- **Script**: Runs the Broken Link Checker recursively and excludes external links.

### Vulnerabilities Check
- **Purpose**: Checks for vulnerabilities in the website using Snyk.
- **Tools**: `snyk`
- **Script**: Runs Snyk test to identify and report vulnerabilities.

### Package Website
- **Purpose**: Packages the website for deployment, caching the build artifacts.
- **Tools**: NPM scripts for building and packaging.
- **Artifacts**: Stores packaged website files for deployment.

### Deploy to Develop
- **Purpose**: Deploys the website to the development environment using Surge.
- **Environment**: Development environment with specific domain configurations.
- **Trigger**: Triggered only on changes to the develop branch.

### Deploy to Release
- **Purpose**: Deploys the website to a release environment with a specific environment name.
- **Actions**: Triggers manual intervention to stop the release environment.
- **Trigger**: Triggered only on release branches.

### Turnoff Release Environment
- **Purpose**: Turns off a release environment manually.
- **Actions**: Teardowns the release environment.
- **Trigger**: Manually triggered and applicable only to release branches.

### Deploy to Production
- **Purpose**: Deploys the website to the production environment using AWS S3.
- **Tools**: AWS CLI for syncing the website files to an S3 bucket.
- **Environment**: Production environment with AWS S3 hosting.
- **Trigger**: Triggered only on changes to the master branch.

## OBS
- Tools like Surge and AWS CLI requires authentication, so i've created protected environment variables with my credentials at my gitlab repository.
