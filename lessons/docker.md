---
path: "/getting-set-up-with-docker"
title: "Getting Set Up with Docker"
order: 3.0
section: "Docker"
---

This is probably why you're here: Docker. Docker is a commandline tool that made creating, updating packaging, distributing, and running containers significantly easier which in turns allowed them become very popular with not just system administraters but the programming populace at large. At its heart, it's a command line very similar to `lxc` that allows you to manage your containers but in a much more convenient way. Let's dive into the core concepts of Docker.

## Docker Desktop

Go ahead and install [Docker Desktop][desktop] right now. It will work for both Mac and Windows. Docker Desktop runs the Docker [daemon][daemon] (daemon just means a program that runs in the background all the time) so that we can download, run, and build containers. If you're on Mac, you'll see a cute little whale icon in your status bar. Feel free to poke around and see what it has. It will also take the liberty of installing the `docker` commandline tool so we can start doing all the fun things with Docker.

## Docker Hub

[Click here][hub] to head over to Docker Hub. Docker Hub is a public registry of pre-made containers. Think of it like an npm for containers. Instead of having to handcraft everything yourself, you can start out with a base container from Docker Hub and start from there. For example, instead of having to start with Ubuntu and install Node.js on it yourself, you can just start with a container that has Node.js already on it! There's a pre-made container for just about anything you can think of, and for those you can't it's pretty easy to find a good starting point so you can make your own bespoke, artisinal containers. If you feel so inclined, you can publish your own containers on the registry so others can take advantage of your discoveries.

Feel free to make an account on Docker Hub at this point. We won't be publishing anything to it during this workshop but it's a good idea to have one for when you want to!

## CLI

Let's take a look at some more cool features of the Docker CLI.

### pull / push

`pull` allows you to pre-fetch container to run. P

```bash
docker pull jturpin/hollywood
docker run -it jturpin/hollywood hollywood # notice it's already loaded and cached here; it doesn't redownload it
```

That will pull the hollywood container from the user jturpin's user account. The second line will execute this fun container which is just meant to look a hacker's screen in a movie (it doesn't really do anything than look cool.)

`push` allows you to push containers to whatever registry you're connected to (probably normally Docker Hub or something like Azure Container Registry).

### inspect

```bash
docker inspect node
```

This will dump out a lot of info about the container. Helpful when figuring out what's going on with a container

### pause / unpause

As it looks, these pauses or unpause all the processes in a container. Feel free to try

```bash
docker run -dit jturpin/hollywood hollywood
docker ps # see container running
docker pause <ID or name>
docker ps # see container paused
docker unpause <ID or name>
docker ps # see container running again
docker kill <ID or name> # see container is gone
```

### exec

This allows you to execute a command against a running container. This is different from `docker run` because `docker run` will start a new container whereas `docker exec` runs the command in an already-running container.

```bash
docker run -dit jturpin/hollywood hollywood
docker ps # grab the name or ID
docker exec <ID or name> ps aux # see it output all the running processes of the container
```

If you haven't seen `ps aux` before, it's a really useful way to see what's running on your computer. Try running `ps aux` on your macOS or Linux computer to see everything running.

### import / export

Allows you to dump out your container to a tar ball (which we did above.) You can also import a tar ball as well.

### history

We'll get into layers in a bit but this allow you to see how this Docker image's layer composition has changed over time and how recently.

```bash
docker history node
```

### info

Dumps a bunch of info about the host system. Useful if you're on a VM somewhere and not sure what the environment is.

```bash
docker info
```

### top

Allows you to see processes running on a container (similar to what we did above)

```bash
docker run mongo
docker top <ID outputted by previous command> # you should see MongoDB running
```

### rm / rmi

If you run `docker ps --all` it'll show all containers you've stopped running in addition to the runs you're running. If you want to remove something from this list, you can do `docker rm <id or name>`.

If you want to remove an image from your computer (to save space or whatever) you can run `docker rmi mongo` and it'll delete the image from your computer. This isn't a big deal since you can always reload it again

### logs

Very useful to see the output of one of your running containers.

```bash
docker run -d mongo
docker logs <id from previous command> # see all the logs
```

### restart

Pretty self explanatory. Will restart a running container

### search

If you want to see if a container exists on Docker Hub (or whatever registry you're connected to), this will allow you to take a look.

```bash
docker search python # see all the various flavors of Python containers you can run
docker search node # see all the various flavors of Node.js containers you can run
```

[ubuntu]: https://hub.docker.com/_/ubuntu
[alpine]: https://hub.docker.com/_/alpine
[node]: https://hub.docker.com/_/node/
[desktop]: https://www.docker.com/products/docker-desktop
[hub]: https://hub.docker.com/search?q=&type=image
[alpine]: https://www.alpinelinux.org/
[daemon]: https://en.wikipedia.org/wiki/Daemon_(computing)
[cgmanager]: https://linuxcontainers.org/cgmanager/