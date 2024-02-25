---
title: Injecting secrets during the build
keywords: concepts, build, images, docker desktop
description: Injecting secrets during the build
---
<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

In this concept, you will learn the following:
- What are Build Secrets?
- How to inject Secrets during the build 

Secrets are sensitive pieces of information like passwords, API keys, or database credentials that your application needs during the build process, but shouldn't be stored within the final image. Injecting these secrets securely ensures both functionality and security for your app

Build secrets like passwords shouldn't be in your Docker image! While build arguments and environment variables are easy, they expose secrets. Instead, use secret mounts or SSH mounts for secure access during the build, ensuring your final image stays safe and sound. Remember, security first!

## Try it out

In this hands-on, you will learn how to use and inject secrets during the build process.


## Setup 

[Download this ZIP file](https://github.com/docker/getting-started-todo-app/blob/build-image-from-scratch/app.zip) and extract the contents into a directory on your machine.


Assuming that you're using a dedicated tool like `AWS Secrets Manager`, `HashiCorp Vault`, or `Azure Key Vault` to manage and inject secrets securely. These tools offer features like access control, rotation, and audit logging, let's create the Dockerfile to mount the encrypted file as a secret during the build process.

### Creating the Dockerfile

Now that you have the project, you are ready to create the `Dockerfile`.


1. Create a file named `Dockerfile` in the same folder as the file `package.json`.

    > **Dockerfile file extensions**
    >
    > It's important to note that the `Dockerfile` has _no_ file extension. Some editors
    > will automatically add an extension to the file (or complain it doesn't have one).
    { .important }

2. In the `Dockerfile`, define your base image by adding the following line:

    ```dockerfile
    FROM node:20-alpine
    ```

3. Now, define the working directory by using the `WORKDIR` instruction:

    ```dockerfile
    WORKDIR /usr/local/app
    ```

4. Copy all of the files from the host into the container by using the `COPY` instruction:

    ```dockerfile
    COPY . .
    ```

5. Install the app's dependencies by using the `yarn` CLI and package manager. You run a command using the `RUN` instruction:

    ```dockerfile
    RUN yarn install --production
    ```

6. Finally, specify the default command to run by using the `CMD` instruction:

    ```dockerfile
    CMD ["node", "./src/index.js"]
    ```

And with that, you should have the following `Dockerfile`:

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
EXPOSE 3000
CMD ["node", "./src/index.js"]
```

## Configuring Secrets

The source of secrets can either be a file or environment variable. You can specify it explicitly with `type=file` or `type=env`.


Let's consider the following secret file:

```console
 cat mysecretfile
 bs-dfhfkdsfh
```

## Creating a Multi-Stage Dockerfile

The following Dockerfile use builder stage for secret usage. It mounts the secrets during the build.
The final stage will have no access to secrets.


```diff
 # syntax = docker/dockerfile:1.3

FROM node:20-alpine AS builder
WORKDIR /app

# Copy your application files and the build script
COPY package.json yarn.lock build-script.sh .

# Install dependencies
RUN yarn install --production

# Mount the secret during the build
RUN --mount=type=secret,id=mysecrets \
    /bin/sh ./script.sh

# Create a new stage for the final image (no secret access)
FROM node:20-alpine
WORKDIR /app

# Copy the application files from the builder stage
COPY --from=builder /app .

# Expose port 3000 for your application
EXPOSE 3000

# Start your application using the entrypoint
CMD ["node", "src/index.js"]
```

## Creating a sample build script

Copy the below content and save it as script.sh.

```diff
 #!/bin/bash

SECRET=$(cat /run/secrets/mysecrets)
```

## Building the image

Use the docker build command with the `--secret` flag to map an environmetna variable directly to a secret ID.

```console
  docker build --secret id=mysecrets,src=mysecretfile . -f Dockerfile -t nodeapp
```

## Running the container

```console
 docker run -d -p 3000:3000 node-app
```

This approach allows you to securely inject secrets into your Node.js app's build process using BuildKit without compromising the security of your sensitive information.


## Additional Resources

- [Build Secrets](https://docs.docker.com/build/building/secrets/)

{{< button text="Troubleshooting Failing Builds" url="troubleshooting-failing-builds" >}}
