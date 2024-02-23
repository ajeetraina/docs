---
title: Troubleshooting failing builds
keywords: concepts, build, images, docker desktop
description: Troubleshooting failing builds
---

Building Docker images is a powerful way to containerize your applications, but sometimes things can go wrong, and builds can fail. This tutorial guides you through the essential steps to identify and resolve common issues encountered during Docker builds.

##  1. Error: "docker buildx build" requires exactly 1 argument

If you encounter the following error message while building the Docker image using `Dockerfile`, the easiest fix is adding `.` at the end of your `docker build` command. 

The `docker buildx build` command requires at least one argument, which is typically the path to the Dockerfile you want to use for the build

```console
 docker buildx build -t node-app .
```

This command assumes your `Dockerfile` is in the current directory. If it's located elsewhere, replace `.` with the actual path to your `Dockerfile`.

## 2. Error: Insufficient Scope, Authorization Failed


In case you encounter the following error message while configuring CI/CD to build Docker image

```console
 buildx failed with: ERROR: failed to solve: failed to push getting-started-todo-app:1.0: push access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
```

Explanation: Double-check both the `DOCKER_USER` and `DOCKER_PAT` secrets values that you configured on GitHub repository.


