---
title: What is a container
keywords: concepts, build, images, container, docker desktop
description: What is a container
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

A `container` is an isolated sandbox environment on your machine. Imagine containers like shipping containers for cargo ships. Each `container` holds its own cargo (application code, libraries, configurations) and is sealed off from other containers. This ensures that even if one container gets damaged or malfunctions, it doesn't affect the contents or functionality of other containers on the same ship (your machine).

While containers are isolated from each other, they share the underlying operating system kernel. This means they are much lighter and more efficient compared to virtual machines (VMs) which require their own complete operating system. This allows you to run more containers on a single machine compared to VMs.

Containers are self-contained and include everything an application needs to run. This makes them highly portable. You can move a container from one machine to another (e.g., from development to production) without worrying about compatibility issues as long as the underlying system supports containerization.

Consider a web application with separate components: frontend, backend, and database. Each component can be packaged in its own container. They can all run on the same machine, but they are isolated from each other. This simplifies development, testing, and deployment as you manage each component independently.

## Try it now

In this hands-on, you will see how to run a simple `Nginx` container using Docker Desktop.

## Run a container

Use the following instructions to run a container.

1. Open Docker Desktop and select the search.
2. Specify `nginx` in the search and then select **Run**.
3. Expand the **Optional settings**.
4. In **Container name**, specify `nginx`.
5. In **Host port**, specify `80`.
   ![Specifying host port 80](nginx-parameters.png?border=true)
6. Select **Run**.
7. View containers on Docker Desktop

![nginx container running](nginx-running.png?border=true)


You just ran a container! You can view it in the **Containers** tab of Docker
Desktop. This container runs a simple web server that displays a simple website.
When working with more complex projects, you'll run different parts in different
containers. For example, a different container for the frontend, backend, and
database. In this walkthrough, you only have a simple frontend container.

8. View the frontend

The frontend is accessible on port 80 of your local host. Select the link in
the **Port(s)** column of your container, or visit
[http://localhost:80](http://localhost:80) in your browser to view it.

![Accessing container frontend from Docker Desktop](nginx-success.png?border=true)

9: Explore your container

Docker Desktop lets you easily view and interact with different aspects of your
container. Try it out yourself. Select your container and then select **Files**
to explore your container's isolated file system.

![Viewing container details in Docker Desktop](nginx-files.png?border=true)

10. Stop your container

The `nginx` container continues to run until you stop it. To stop
the container in Docker Desktop, go to the **Containers** tab and select the
**Stop** icon in the **Actions** column of your container.

![Stopping a container in Docker Desktop](nginx-stopped.png?border=true)

In this walkthrough, you ran a pre-made image and explored a container. In addition to running pre-made images, you can build and run your own application as container.

## Additional resources

- [What is a container](https://docs.docker.com/guides/walkthroughs/what-is-a-container/)
- [Overview of container](https://www.docker.com/resources/what-container/)
- [Why Docker?](https://www.docker.com/why-docker/)

{{< button text="What is an image" url="what-is-an-image" >}}
