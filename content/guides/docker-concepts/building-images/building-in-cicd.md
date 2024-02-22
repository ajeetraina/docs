---
title: Building in CI/CD
keywords: concepts, build, images, docker desktop
description: Building in CI/CD
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

In this concept, you will learn the following:

- How to setup and use GitHub Actions to build and test your Docker image
- How to push the Docker image to the registry

GitHub Actions is one of the popular continuous integration and continuous delivery(CI/CD) platform that allows you to automate your build, test and deployment pipeline. It allows you to create workflows that build and test every pull requests to your repository, or merge pull requests to the production.

Building in CI involves the following steps:

* Create a new repository on GitHub
* Define the GitHub Actions workflow
* Run the workflow

### Getting Started 

In this section, you'll learn how to set up and use GitHub Actions to build and test your Docker image as well as push it to Docker Hub. You will complete the following steps:



## Create the repository

Create a GitHub repository, configure the Docker Hub secrets, and push your source code.



1. Configuring the repository

Open the GitHub project repository` Settings`, and go to `Secrets and variables > Actions. `Create a new secret named `DOCKER_USER` and your Docker ID as value.

![rep config](configuring-repo.png)

2. Create a new Personal Access Token (PAT) for Docker Hub

Add the PAT as a second secret in your GitHub repository, with the name` DOCKER_PAT`.


## Define the GitHub Actions workflow

Let’s follow the steps below to set up the GitHub Actions workflow for building, testing, and pushing the image to Docker Hub. 



1. Open [https://github.com/docker/getting-started-todo-app](https://github.com/docker/getting-started-todo-app) and click on “Actions”
2.  Click on the “set up a workflow yourself” link.

![github action](github_action.png)

3. This creates an empty  .github/workflows directory in your project root.
4. Add the following content into the YAML file. You can name this file anything you like.

```console
name: ci

on:
  push:
    branches:
      - "main"

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USER }}
          password: ${{ secrets.DOCKER_PAT }}
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          target: final
          tags: ${{ secrets.DOCKER_USER }}/${{ github.event.repository.name }}:latest
      
```

The following workflow automates the process of building and pushing a Docker image when code is pushed to the main branch of the repository. It uses Docker Hub for registry storage and leverages Docker Buildx for efficient multi-platform image building.

Here's a breakdown of the GitHub Actions workflow:



1. **Workflow Name:**

ci: This name suggests it's a continuous integration workflow, likely intended to build and test code changes as they're made.



2. **Triggers:**

on: push: The workflow will be triggered when code is pushed to the repository.

branches: - "main": It will specifically run when code is pushed to the main branch.



3. **Jobs:**

docker: This job contains the steps for building and pushing a Docker image.

runs-on: ubuntu-latest: The job will run on a virtual machine with the latest Ubuntu OS.


## Steps:



1. **Checkout:**
* uses: actions/checkout@v4: This step checks out the code from the repository to the virtual machine.
2. **Log in to Docker Hub:**
* uses: docker/login-action@v3: Logs in to Docker Hub using provided credentials.
* username: ${{ secrets.DOCKER_USER }}: Retrieves the username from a secret named DOCKER_USER.
* password: ${{ secrets.DOCKER_PAT }}: Retrieves the password from a secret named DOCKER_PAT.
3. **Setup Docker Buildx:**
* **uses: docker/setup-buildx-action@v3**: Sets up Docker Buildx for building multi-platform images.
4. **Build and push:**
* uses: docker/build-push-action@v5: Builds and pushes the Docker image.
* context: .: Uses the current directory as the build context.
* target: specifies the build target within the Dockerfile
* tags: defines the image tag for the  built image. It dynamically uses the username from the secrets and the repository name from the event context t create a unique tag.

## Run the workflow

Save the workflow file and run the job.

![github workflow](github_workflow.png)

When the workflow is complete, go to your repositories on Docker Hub.If you see the new repository in that list, it means the GitHub Actions successfully pushed the image to Docker Hub ! 🎉

### Additional Resources

To learn more about building in CI/CD, visit the following resources:

- [Configuring CI/CD for your Node.js application](https://docs.docker.com/language/nodejs/configure-ci-cd/)
- [Configuring CI/CD for your Rust application](https://docs.docker.com/language/rust/configure-ci-cd/)
- [Configuring CI/CD for your Python application](https://docs.docker.com/language/python/configure-ci-cd/)
- [Configuring CI/CD for your Java application](https://docs.docker.com/language/java/configure-ci-cd/)


Now that you have learned about building and publishing images to Docker Hub using CI/CD, it's time to learn how to make your Docker builds faster and more efficient using build cache.


{{< button text="Using the Build Cache" url="using-the-build-cache" >}}
