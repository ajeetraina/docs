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


## Step 1. Modify your Dockerfile

Assuming that you're using a dedicated tool like `AWS Secrets Manager`, `HashiCorp Vault`, or `Azure Key Vault` to manage and inject secrets securely. These tools offer features like access control, rotation, and audit logging, let's modify the Dockerfile to mount the encrypted file as a secret during the build process:

```diff
FROM node:20-alpine
WORKDIR /app
EXPOSE 3000
# Mount secret files during build
RUN --mount=type=secret,id=MYSQL_CREDS \
    npm  install
RUN --mount=type=secret,id=MYSQL_CREDS \
    node build.js
CMD ["node", "./src/index.js"]
```


### Step 2. Specify secrets ID and their encrypted file locations:

Use the docker build command with the `--secret` flag to specify the secret ID and its encrypted file location.

```console
docker build \
    --secret id=MYSQL_CREDS,src=/path/to/encrypted_mysql_creds \
    -t your_todo_list_app .
```

By default, secrets are mounted to /run/secrets/<id>. You can customize the mount point in the build container using the target option in the Dockerfile. In the following example, you mounted the secret to /path/to/encrypted_mysql_creds file in the build context.

Replace placeholders with your actual information:

- `MYSQL_CREDS`: Replace this with the actual ID you choose for your secret.
- `/path/to/encrypted_mysql_creds`: Replace this with the location of your encrypted MySQL credentials file.


## Step 3. Running the container

```console
 docker run -d -p 3000:3000 todo-list-app
```

## Step 4. Verify Secret access

Inside the running container, access the secret file or environment variable depending on how your application retrieves it. For example, in our case, the secret is mounted to /run/secrets/MYSQL_CREDS, you could check its contents with:

```console
 cat /run/secrets/MYSQL_CREDS
```
This approach allows you to securely inject secrets into your Node.js app's build process using BuildKit without compromising the security of your sensitive information.


## Additional Resources

- [Build Secrets](https://docs.docker.com/build/building/secrets/)

{{< button text="Troubleshooting Failing Builds" url="troubleshooting-failing-builds" >}}
