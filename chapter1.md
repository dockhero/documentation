# Quickstart

See Heroku dev center article for an official quick-start guide. Below is a short version:

```bash
$ heroku addons:create dockhero        # provision the add-on
$ heroku plugins:install dockhero      # install CLI plugin
$ heroku dh:generate helloworld        # prepare dockhero-compose.yml
$ heroku dh:compose up -d              # run the stack  
```

## Provisioning the add-on

```bash
$ heroku addons:create dockhero
```

It takes 2-3 minutes to spin up and configure an EC2 instance with Docker server and monitoring tools. You can track the provisioning status in add-on dashboard. When the provisioning is done, the following environment variables are set in Heroku config:

* DOCKHERO\_HOST - this is the address of the machine. It can be used to connect to the services you will launch there
* DOCKHERO\_CERTS\_URL - this one is used internally by the CLI plugin to download the certificates and connect to Docker
* DOCKHERO_FULL_SSL_URL and DOCKHERO_FLEXIBLE_SSL_URL - two HTTP/2 SSL endpoints which proxy traffic to your stack (see [SSL Endpoints](/ssl-termination.md))


## Installing CLI plugin

```bash
$ heroku plugins:install dockhero
```

The plugin configures your Docker client to talk to Dockhero rather than your default machine. Most of the time you will use `heroku dh:compose` shortcut. See other commands in CLI Plugin docs.

## Prepare dockhero-compose.yml

```bash
$ heroku dh:generate helloworld 
```

This command writes a stack definition into `dockhero-compose.yml`:

```yaml
# dockhero-compose.yml
version: "2"
services:
 web:
   image: dockhero/dockhero-docs:hello
   ports:
     - "80:8080"
```

See a list of available generators [here.](https://github.com/dockhero/generators)

## Running the stack

```bash
$ heroku dh:compose up -d
Creating network "dockhero_default" with driver "bridge"
Creating dockhero_web_1

$ heroku dh:compose ps
Name              Command                        State        Ports
-----------------------------------------------------------------------------------
dockhero_web_1    /bin/sh -c http-server /app    Up      54.174.36.199:80->8080/tcp

$ heroku logs -p dockhero --tail
```

This launches your stack on the EC2 instance.

TODO: Limits

