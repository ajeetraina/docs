---
title: Troubleshooting failing builds
keywords: concepts, build, images, docker desktop
description: Troubleshooting failing builds
---
<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

In this concept, you will learn the following:
- how to troubleshooting common errors during the image building process

Building Docker images is a powerful way to containerize your applications, but sometimes things can go wrong, and builds can fail. This tutorial guides you through the essential steps to identify and resolve common issues encountered during Docker builds.

###  1. Error: "docker buildx build" requires exactly 1 argument

If you encounter the following error message while building the Docker image using `Dockerfile`, the easiest fix is adding `.` at the end of your `docker build` command. 

The `docker buildx build` command requires at least one argument, which is typically the path to the Dockerfile you want to use for the build

```console
 docker buildx build -t node-app .
```

This command assumes your `Dockerfile` is in the current directory. If it's located elsewhere, replace `.` with the actual path to your `Dockerfile`.

### 2. Error: Insufficient Scope, Authorization Failed


In case you encounter the following error message while configuring CI/CD to build Docker image

```console
 buildx failed with: ERROR: failed to solve: failed to push getting-started-todo-app:1.0: push access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
```

Explanation: Double-check both the `DOCKER_USER` and `DOCKER_PAT` secrets values that you configured on GitHub repository.


