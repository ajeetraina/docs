---
title: What is a container
keywords: concepts, build, images, container, docker desktop
description: What is a container
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

Imagine a library specifically for software components called containers. A container registry is a service that allows you to store, share, and manage these container images. You can think of container registry like a central repository where developers can find pre-built containers for various software, upload their own creations, and collaborate with others.

[Docker Hub](https://hub.docker.com), created by Docker, is the leading container registry and one of the most popular options. It is the world’s largest repository of container images with an array of content sources including container community developers, open source projects, and independent software vendors (ISV) building and distributing their code in containers. It is a service provided by Docker for finding and sharing container images.

### Key Features of Docker Hub

- [Repositories](https://docs.docker.com/docker-hub/repos/): Push and pull container images.
- [Builds](https://docs.docker.com/docker-hub/builds/): Automatically build container images from GitHub and Bitbucket and push them to Docker Hub.
- [Webhooks](https://docs.docker.com/docker-hub/webhooks/): Trigger actions after a successful push to a repository to integrate Docker Hub with other services.
- [Docker Hub CLI tool](https://github.com/docker/hub-tool#readme)  and an API that allows you to interact with Docker Hub.
- Browse through [the Docker Hub API](https://docs.docker.com/docker-hub/api/latest/) documentation to explore the supported endpoints.

## Try it now


### Step 1: Sign up for a free Docker account

Start by creating a [Docker ID](https://hub.docker.com/signup).

A Docker Hub id grants you access to Docker Hub repositories and lets you explore available images from the community and verified publishers. You also need a Docker ID to share images on Docker Hub.

### Step 2: Create your first repository

To create a repository:

1. Sign in to [Docker Hub](https://hub.docker.com).
2. On the Repositories page, select **Create repository**.
3. Name it **&lt;your-username&gt;/my-private-repo**.
4. Set the visibility to **Private**.
5. Select **Create**.

You've created your first repository.

### Step 3: Download and install Docker Desktop

You need to [download Docker Desktop](https://www.docker.com/products/docker-desktop/) to build, push, and pull container images.

1. Download and install Docker Desktop

2. Sign in to Docker Desktop using the Docker ID you created in step one.

### Step 4: Pull and run a container image from Docker Hub

1. In your terminal, run `docker pull hello-world` to pull the image from Docker Hub. You should see output similar to:

   ```console
   $ docker pull hello-world
   Using default tag: latest
   latest: Pulling from library/hello-world
   2db29710123e: Pull complete
   Digest:   sha256:7d246653d0511db2a6b2e0436cfd0e52ac8c066000264b3ce63331ac66dca625
   Status: Downloaded newer image for hello-world:latest
   docker.io/library/hello-world:latest
   ```

2. Run `docker run hello-world` to run the image locally. You should see output similar to:

    ```console
    $ docker run hello-world
    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
     (amd64)
     3. The Docker daemon created a new container from that image which runs the
     executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent
     it to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
     $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
     https://hub.docker.com/

    For more examples and ideas, visit:
     https://docs.docker.com/get-started/
    ```

### Step 5: Build and push a container image to Docker Hub from your computer

1. Start by creating a `Dockerfile` to specify your application as shown below:

   ```dockerfile
   FROM busybox
   CMD echo "Hello world! This is my first Docker image."
   ```

2. Run `docker build -t <your_username>/my-private-repo .` to build your Docker
   image.

3. Run `docker run <your_username>/my-private-repo` to test your
Docker image locally.

4. Run `docker push <your_username>/my-private-repo` to push your Docker image to Docker Hub. You should see output similar to:

   ```console
   $ cat > Dockerfile <<EOF
   FROM busybox
   CMD echo "Hello world! This is my first Docker image."
   EOF
   $ docker build -t mobythewhale/my-private-repo .
   [+] Building 1.2s (5/5) FINISHED
   => [internal] load build definition from Dockerfile
   => => transferring dockerfile: 110B
   => [internal] load .dockerignore
   => => transferring context: 2B
   => [internal] load metadata for docker.io/library/busybox:latest
   => CACHED [1/1] FROM docker.io/library/busybox@sha256:a9286defaba7n3a519
   => exporting to image
   => => exporting layers
   => => writing image sha256:dcdb1fd928bf257bfc0122ea47accd911a3a386ce618
   => => naming to docker.io/mobythewhale/my-private-repo
   ```

   ```console
   $ docker run mobythewhale/my-private-repo
   Hello world! This is my first Docker image.
   $ docker push mobythewhale/my-private-repo
   The push refers to repository [docker.io/mobythewhale/my-private-repo]
   d2421964bad1: Layer already exists
   latest: digest: sha256:7604fbf8eeb03d866fd005fa95cdbb802274bf9fa51f7dafba6658294
   efa9baa size: 526
   ```

    >**Note**
    >
    > You must be signed in to Docker Hub through Docker Desktop or the command line, and you must also name your images correctly, as per the above steps.

5. Your repository in Docker Hub should now display a new `latest` tag under **Tags**:


In this guide, you learned how to sign up for a Docker Hub account, created your first Docker Hub repository, pulled an existing "hello world" image, built your own container image and pushed it to the Docker Hub

{{< button text="What is Docker Compose" url="what-is-Docker-Compose" >}}
