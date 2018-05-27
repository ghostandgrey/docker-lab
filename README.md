# Docker Lab instructions
Please note, this tutorial requires you to have Docker Community Edition installed on your computer.  Get it [here](https://www.docker.com/community-edition).

## 1. Docker Hello World
Please note: if it seems like a lot is being introduced right off the bat, it's just to expose you to it.  We will be exploring everything touched on here in greater details as the tutorial proceeds.

On the command line, type in:
```
docker run hello-world
```

You will see the following output:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
 ```
 
The description of what happened is a pretty good summary.  But here are some more details:
1. The Docker client, invoked via the command line contacts the Docker daemon running on your system.
2. The Docker daemon pulls the "hello-world" image.
   * Docker is by default configured to search Docker Hub for images, as opposed to say, your organization's private repo.
   * In order to specify a tag for an image, you would append the tag name with a colon after the image name, such as
     ```docker run hello-world:linux```
     If you do not specify a tag, then Docker will treat it as if you requested the "latest" version of the image, as in
     ```docker run hello-world:latest```
     The "latest" tag is what Docker automatically tags images with when you do not explicitly provide one at build time.
     ```docker build my-container``` is equivalent to ```docker build my-container:latest```.  We will explore well-known problems with the "latest" tag in a bit.
3. The Docker daemon creates a new container based on the "hello-world" image, and starts it.  In fact, the ```docker run``` command is a shorthand for two commands: ```docker create``` (which instantiates the container from the image) and ```docker start <image>``` (which actually runs it).
4. The Docker daemon streams the output to the Docker client, which in turn sends it to your CLI.  By default, Docker will stream a container's output to your terminal.  You can ensure that Docker does not output to your terminal by using the -d or --detach flag, as in: ```docker run -d hello-world```.  You can think of the default as running a command in linux, outputting to the terminal vs. appending the command with an ampersand, which backgrounds the process and does not attach its output to your terminal.  i.e. ```top``` vs. ```top &```.

## 2. Docker Hub
Here is the URL for the Docker Hub page for the hello-world image (this page is its "repository"): https://hub.docker.com/_/hello-world/  -- It is worth familiarising yourself with the layout and content of Docker Hub pages.

![Docker Hub](/images/dockerhub.png)

1. I find the _Tags_ page to be a much better and clearer listing of a repository's tags.  Those in the _Full Description_ section are manually entered while those on the _Tags_ page come from Docker itself.
![Docker Hub Tags page](/images/dockerhubtags.png)
2. You are always provided with the command needed to pull an image, similar to how you can get a git repo's link to clone it locally.
3. The _Full Description_ will provide a lot of interesting details about images.  It is common for the repository's maintainers to provide links to the Dockerfile(s) used to create the image.  This is in keeping with the open-source nature of a lot of Docker work - you can see for yourself exactly what is and is not in an image.  The content and quality of the _Full Description_ is going to vary by the maintainer(s).  My experience has been that "official" repos for products, e.g. Docker-related repos, Redis, Wordpress, etc. tend to have the best documentation.
