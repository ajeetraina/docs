---
title: Multi-container applications
keywords: concepts, build, images, docker desktop
description: Multi-container applications
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

In this concept, you will learn the following:
- How to add database container to the application stack
- How to run multi-container applications

Traditionally, applications might be packaged with all their dependencies into a single unit. While this approach can be simple, it has limitations:

- **Scalability**: Scaling individual components like a database becomes difficult, as you'd have to scale the entire application.
- **Versioning**: Updating one component might require rebuilding the entire application, even if other components remain unchanged.
- **Maintainability**: Troubleshooting issues becomes more complex when dealing with intertwined components.

### Benefits of Separate Containers

- **Microservices Architecture**: Each container acts as a self-contained microservice, promoting scalability and independent development.
- **Isolation**: Applications run in isolated environments, improving security and preventing conflicts.
- **Flexibility**: You can easily update, restart, or scale individual containers without impacting others.
