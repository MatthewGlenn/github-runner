# Github self-hosted runner Dockerfile and Kubernetes configuration

**This is a fork of @SanderKnape's repo that builds the github-runner automatically**

[![Actions Status](https://github.com/actions/runner/workflows/Runner%20CI/badge.svg)](https://github.com/matthewglenn/github-runner/actions)

![Image Version](https://ghcr-badge.egpl.dev/matthewglenn/github-runner/latest_tag?color=%2344cc11&ignore=latest&label=latest&trim=)


This repository contains a Dockerfile that builds a Docker image suitable for running a [self-hosted GitHub runner](https://sanderknape.com/2020/03/self-hosted-github-actions-runner-kubernetes/). A Kubernetes Deployment file is also included that you can use as an example on how to deploy this container to a Kubernetes cluster.

## Building the container

`docker build -t github-runner .`

## Features

* Repository runners
* Organizational runners
* Labels
* Graceful shutdown
* Support for installing additional debian packages
* Auto-update after the release of a new version

## Examples

Register a runner to a repository.

```sh
docker run --name github-runner \
     -e GITHUB_OWNER=username-or-organization \
     -e GITHUB_REPOSITORY=my-repository \
     -e GITHUB_PAT=[PAT] \
     ghcr.io/matthewglenn/github-runner:latest
```

Register a runner with github token.

```sh
docker run --name github-runner \
     -e GITHUB_OWNER=username-or-organization \
     -e GITHUB_REPOSITORY=my-repository \
     -e GITHUB_TOKEN=[github.token] \
     ghcr.io/matthewglenn/github-runner:latest
```

Create an organization-wide runner.

```sh
docker run --name github-runner \
    -e GITHUB_OWNER=username-or-organization \
    -e GITHUB_PAT=[PAT] \
    ghcr.io/matthewglenn/github-runner:latest
```

Set labels on the runner.

```sh
docker run --name github-runner \
    -e GITHUB_OWNER=username-or-organization \
    -e GITHUB_REPOSITORY=my-repository \
    -e GITHUB_PAT=[PAT] \
    -e RUNNER_LABELS=comma,separated,labels \
    ghcr.io/matthewglenn/github-runner:latest
```

Install additional tools on the runner.

```sh
docker run --name github-runner \
    -e GITHUB_OWNER=username-or-organization \
    -e GITHUB_REPOSITORY=my-repository \
    -e GITHUB_PAT=[PAT] \
    -e ADDITIONAL_PACKAGES=firefox-esr,chromium \
    ghcr.io/matthewglenn/github-runner:latest
```
