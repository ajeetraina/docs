---
title: Configuring containers
keywords: concepts, build, images, docker desktop
description: Configuring containers
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

Building Docker images provides the foundation for running applications in containers. However, configurations are essential for fine-tuning their behavior and data management. This section dives deeper into core configuration techniques for Docker containers.

## Configuring containers: Memory, CPUs and GPUs

Imagine a containerized application that consumes all available memory on the host. This could lead to an "Out-Of-Memory" (OOM) exception, potentially crashing the Docker daemon and other crucial system processes. Similarly, exceeding CPU limits can slow down other containers or even the entire system. For applications requiring graphical processing power (GPUs), uncontrolled access can lead to performance bottlenecks for other GPU-dependent tasks.


In the world of containerization, efficient resource management is essential. By setting appropriate limits on memory, CPU, and GPUs, you can ensure smooth operation for your containers and prevent them from hogging resources on the host machine. This tutorial will guide you through configuring these essential settings for optimal container performance.


## Try it now

In this hands-on, you'll see how to configure containers for resources like CPU and Memory.
### Setup

[Download this ZIP file](https://github.com/docker/getting-started-todo-app/blob/build-image-from-scratch/app.zip) and extract the contents into a directory on your machine.

### Step 1. Create a file named Dockerfile

Create a file named Dockerfile in the same folder as the file package.json

```diff
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN yarn install --production
COPY . .
EXPOSE 3000
CMD ["node", "./src/index.js"]
```

### 2. Build the Image

Open a terminal in the directory containing your modified Dockerfile and run:

```console
docker build -t myapp .
```

### 3. Run the Container (with Configurations)

Let's modify the docker run command to configure memory and CPU for your sample todo-list application:

```console
docker run -p 3000:3000 \
  -m 256m --cpus=0.75
  myapp
```

This command allocates a maximum of `256` megabytes of memory and assigns a `0.75` CPU share to your container. Adjust these values based on your application's requirements and available resources on your host machine.

> **Important Considerations**
>
> - `Testing and Monitoring`: Always test your application's resource needs to determine appropriate limits. Use tools like `docker stats` to  monitor resource usage by your containers.
> - `Finding the Balance`: Striking a balance between resource allocation and optimal performance is crucial. Too high limits can lead to underutilization, while overly restrictive limits might hinder performance.
{ .information }

By effectively configuring CPU, memory, and GPUs for your containers, you can achieve efficient resource management within your Docker environment. Remember, the ideal configuration will vary depending on your specific application and hardware setup. Utilize the provided options and best practices to fine-tune your container configuration for optimal performance.

## Additional resources

- [Resource Constraints](https://docs.docker.com/config/containers/resource_constraints/)


Now that you have learned about configuring container for resource, it's time to learn how to override container defaults.

{{< button text="Overriding container defaults" url="overriding-container-defaults" >}}
