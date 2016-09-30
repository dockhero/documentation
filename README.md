# Overview

Dockhero is an add-on which turns any Docker image into a microservice attached to your Heroku app

If you think of Heroku add-ons in general as of boxes with some useful mechanisms inside \(like databases, log analyzers, messengers etc.\), then Dockhero is an empty box where you can put your own mechanism described by [docker-compose.yml](https://docs.docker.com/compose/compose-file/).

![](https://static.tildacdn.com/tild3434-6163-4238-a463-623133313634/heroku_dockhero_2_padding.png)

When you add Dockhero add-on to your Heroku application, a new Docker cluster \(currently consisting of a single Swarm master\) is provisioned, and it's address is exposed to your Heroku app via DOCKHERO\_HOST environment variable.

## CLI

We developed a CLI plugin which makes your Docker client talk to Dockhero instead of your default machine:

```bash
$ heroku dh:sh          
Now DOCKER is configured with Dockhero's Swarm endpoint 
This is a temporary change affecting the current shell session only

sh$ docker ps
CONTAINER   ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES
```

Whenever in your console you need to simultaneously use Dockhero and the local Docker, you can use shortcuts:

```
heroku dh:docker <command>            # execute docker <command> on Dockhero cluster
heroku dh:compose <command>           # call docker-compose <command> on Dockhero cluster
```

The `dh:compose` shortcut assumes that your stack is named `dockhero-compose.yml`.

It also makes your Heroku environment variables available via variables substitution, so that you don't have to commit

## More than "just Docker"

Dockhero comes with a few features which help your microservice fit comfortably into Heroku ecosystem:

* **The logs are streamed into Heroku logs.** If for some reason you want to run apache or nginx as a microservice, you'll find  access.log \/ error.log among your Heroku logs; 
* **Heroku environment variables are available in dockhero-compose.yml. **This way you store the configuration of your microservice "the Heroku way" and don't commit your secrets into git.
* **Monitoring and Alerts. **You'll be notified if your app consumes more than 90% of available memory or disk space. You can enable Newrelic integration to get detailed resource usage history.
* **CDN and SSL termination. **This is especially useful when you consume the microservice directly from the front-end
* **EBS volumes with daily backups.** This is currently under development. We created a volume driver which mounts your Docker volumes to Amazon's EBS.

