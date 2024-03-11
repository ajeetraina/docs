---
title: Persisting container data
keywords: concepts, build, images, docker desktop
description: Persisting container data
---

<iframe width="650" height="365" src="https://www.youtube.com/embed/nsWWQ1xoEy0?rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Explanation

In this concept, you will learn the following:
- How to persist data using named volume
- How to persist data using Bind Mount


By default, containers are considered stateless. This means they don't maintain any state (data) between executions. Any changes made to data within a container are lost once the container stops. Containers are designed to be short-lived and disposable.  When a container finishes its task or is stopped, all its data disappears unless you take steps to persist it.

Sometimes, you may want to persist the data that a container generates. Docker has two options for containers to store files on the host machine, so that the files are persisted even after the container stops: volumes, and bind mounts.

## Volumes


Volumes provide the ability to connect specific filesystem paths of the container back to the host machine. If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

When you mount a volume, it may be named or anonymous. Anonymous volumes are given a random name that's guaranteed to be unique within a given Docker host. Anonymous volumes are not managed by Docker and are scoped to a single container. They are destroyed when the container is removed. Anonymous volumes are implicitly created when you use the `-v` flag or the `--mount` option with Docker commands without specifying a volume name.


## Named Volumes


Named volumes are managed by Docker and have a user-defined name. They can be shared across multiple containers and persist even after the container using them is removed. Named volumes are explicitly created using the `docker volume create` command or the `docker run` command with the `--volume-driver` option and a specific driver.

Compared to anonymous volumes that are only visible to the container they are mounted in, Named volumes can be mounted into multiple containers at the same time, allowing them to share data.

| Feature | Volumes | Named Volumes |
|-----|------|-----|
| Scope | Single container | Multiple containers |
| Creation | Implicit | Explicit(`docker volueme create` |
| Visbility | Single container | Multiple containers(shared) |
| Management | No specific commands | List, inspect, prune, remove commands|



## Bind Mounts

Bind mounts have limited functionality compared to volumes. When you use a bind mount, a file or directory on the host machine is mounted into a container. The file or directory is referenced by its full path on the host machine. The file or directory doesn't need to exist on the Docker host already. It is created on demand if it doesn't yet exist. Bind mounts are fast, but they rely on the host machine's filesystem having a specific directory structure available. If you are developing new Docker applications, consider using named volumes instead. You can't use Docker CLI commands to directly manage bind mounts.

| Feature | Named Volumes | Bind Mounts |
|-----|------|-----|
| Host Location | Docker chooses | You control |
| Mount Example(using `-v`) | my-volume:/usr/local/data | /path/to/data:/usr/local/data |
| Populates new volume with container contents | Yes | No|
| Supports Volume Drivers | Yes | No |

## Try it out

In this hands-on, you will see how to persist data between containers using Bind Mounts

### Setup

If you have git, you can clone the repository for the sample application. Otherwise, you can download the sample application. Choose one of the following options.

{{< tabs >}}
{{< tab name="Clone with git" >}}

Use the following command in a terminal to clone the sample application repository.

```console
$ git clone https://github.com/docker/getting-started-todo-app
```

{{< /tab >}}
{{< tab name="Download" >}}

Download the source and extract it.

{{< button url="https://github.com/docker/getting-started-todo-app/blob/build-image-from-scratch/app.zip" text="Download the source" >}}

{{< /tab >}}
{{< /tabs >}}

### Step 1. Create a new Dockerfile

Create a file named `Dockerfile.single` in the same folder as the file package.json

```diff
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN yarn install --production
COPY . .
EXPOSE 3000
CMD ["node", "./src/index.js"]
```

### Step 2. Build the Image

Open a terminal in the directory containing your modified Dockerfile and run:

```console
docker build -t myapp . -f Dockerfile.single
```

### Step 3. Run the Container


```console
docker run -dp 3000:3000 \
 -w /app -v "$(pwd):/app" \
  myapp \
  sh -c "yarn install && yarn run dev"
```

- `-dp 3000:3000` - Run in detached (background) mode and create a port mapping
- `w /app` - sets the container's present working directory where the command will run from
- `-v "$(pwd):/app"` - bind mount (link) the host's present /app directory to the container's /app directory. Note: Docker requires absolute paths for binding mounts, so in this example we use pwd for printing the absolute path of the working directory, i.e. the app directory, instead of typing it manually
- `myapp` - the image to use. Note that this is the base image for our app from the Dockerfile
- `sh -c "yarn install && yarn run dev"` - the command. We're starting a shell using sh (alpine doesn't have bash) and running yarn install to install all dependencies and then running yarn run dev. If we look in the package.json, we'll see that the dev script is starting nodemon.

### Step 4. Watch the logs

```
 docker logs -f <container-id>
```

### Modify the app

Let's make a change to the app. In the `src/statis/js/index.js file, let's change the "Add Item" button to simply say "Add". This change will be on line 109 - remember to save the file.

```diff
 -                         {submitting ? 'Adding...' : 'Add Item'}
 +                         {submitting ? 'Adding...' : 'Add'}
```

Simply refresh the page (or open it) and you should see the change reflected in the browser almost immediately. It might take a few seconds for the Node server to restart, so if you get an error, just try refreshing after a few seconds.

![todo](todoapp.png)

Using bind mounts is very common for local development setups. The advantage is that the dev machine doesn't need to have all of the build tools and environments installed. With a single docker run command, the dev environment is pulled and ready to go. 

## Additional resources

- [Persist container data](https://docs.docker.com/guides/walkthroughs/persist-data/)
- [Run multi-container applications](https://docs.docker.com/guides/walkthroughs/multi-container-apps/)

Now that you have learned about persisting container data, it's time to learn how to share local files with containers.

{{< button text="Sharing local files with containers" url="sharing-local-files" >}}
