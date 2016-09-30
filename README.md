# Introduction

Dockhero is an add-on which turns any Docker image into a microservice attached to your Heroku app

If you think of Heroku add-ons in general as of boxes with some useful mechanisms inside \(like databases, log analyzers, messengers etc.\), then Dockhero is an empty box where you can put your own mechanism described by [docker-compose.yml](https://docs.docker.com/compose/compose-file/).

![](https://static.tildacdn.com/tild3434-6163-4238-a463-623133313634/heroku_dockhero_2_padding.png)

When you add Dockhero add-on to your Heroku application, a new Docker cluster \(currently consisting of a single Swarm master\) is provisioned. In order to get your Docker CLI tools configured to use that cluster, you can use our **"dh"** CLI Plugin:

```bash
$ heroku dh:sh          
Now DOCKER is configured with Dockhero's Swarm endpoint 
This is a temporary change affecting the current shell session only

sh$ docker ps
CONTAINER   ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES
```

If in your console you need to quickly switch between the local Docker and Dockhero, you can use shortcuts: 

```
heroku dh:docker <command>            # call docker <command> on Dockhero cluster
```





