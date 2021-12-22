---
date: 2017-07-18
title: "Useful Docker Commands/Tips"
author: Bailey Everts
---

TL:DR Skip to the bottom, copy and paste snippet into your .bash_profile.

Here are a handful of tips and commands I have compiled from my time working with docker.

### Tips
Targeting Containers, Images, etc
When interacting with the docker api (via the cli or any other means), you only need to use the unique piece of the id for what you are targeting. That is to say if these are my containers:
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES  
3c273e91180b        postgres            "docker-entrypoint..."   5 seconds ago       Up 4 seconds        5432/tcp            wonderful_jones  
a11b6b51aeed        postgres            "docker-entrypoint..."   5 seconds ago       Up 4 seconds        5432/tcp            gifted_hamilton  
```

I could use the command docker logs 3 to show me the logs from the first container (since my second container id starts with a and I only have 2 containers)

### Chaining Commands
I have seen lots of crazy grep/awk commands in order to grab bits of information from the docker cli output. Docker provides some flags across many popular commands so that this is completely unnecessary.

* `-q/--quiet` - This can be used to force the output of your command to only output ids, this means we can use this flag to get an output in a format ready to pipe into another command. Works on: images, ps, network ls, volume ls, and more
* `-f/--filter` - This can be used to apply a filter on the output of the command to return a subset of the items that would otherwise be output
Using the -q and -f flags we can chain most docker commands together in readable fashion.

### Useful Commands
Warning: I swing a heavy hammer with my docker environments since they are meant to be ephemeral, if you don't want to lose things in your environment be careful with these commands.

#### Kill all containers
`docker kill -f $(docker ps -aqf status=running)` - This can be read as "Forcefully kill (docker kill -f) all running containers (docker ps -aqf status=running)". This command will kill all running containers without prompting.

What is the difference between stop and kill?

stop will try to shutdown nicely by sending the shutdown signal to the container while kill will forcibly shutdown all containers without waiting for a graceful exit.

#### Remove all exited containers
`docker rm -f $(docker ps -aqf status=exited)` - This can be read as "Forcefully remove (docker rm -f) all exited containers (docker ps -aqf status=exited)". This command will remove all exited containers without prompting.

#### Remove all images
`docker rmi -f $(docker images -q)` - This can be read as "Forecfully remove (docker rmi -) all images". This command will try to remove all images without prompt. If any images have containers (in any state), those containers will need to be removed before the images can be removed.

#### Remove all of other things
You can use the pattern shown above to cleanup networks, volumes, services, and/or whatever other docker modules you use.

#### Open a shell session into a container
`docker exec -it CONTAINER_ID sh` - This can be read as "Execute the command sh in the container with the id CONTAINER_ID in interactive mode. Often times I hear someone say "how can I ssh into a container?", this isn't using the ssh protocol, but it is effectively the same thing.

Note: If you want to use bash you can replace sh with bash, keep in mind that not all images will have bash installed (alpine for instance does not come with bash by default).

### Aliases
You can pop this in your ~/.bash_profile to get easy access to the operations described above:

```
# kill all running containers
alias dkill='docker kill $(docker ps -aqf status=running)'  
# remove all exited containers
alias drm='docker rm -f $(docker ps -aqf status=exited)'  
# kill and remove all containers
alias drmf='dkill && drm'  
# remove all images
alias drmi='docker rmi -f $(docker images -q)'  
# open a shell session into container - `dsh SOMEID`
dsh() {  
  docker exec -it ${1} sh
}
```
