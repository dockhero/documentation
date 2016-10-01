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

It takes 2-3 minutes to spin up and configure an EC2 instance with Docker server and monitoring tools. You can track the provisioning status in add-on dashboard. When the provisioning is done, two environment variables are set in Heroku config:

* DOCKHERO\_HOST - this is the address of the machine. It can be used to connect to the services you will launch there
* DOCKHERO\_CERTS\_URL - this one is used internally by the CLI plugin to download the certificates and connect to Docker

## Installing CLI plugin

```bash
$ heroku plugins:install dockhero
```

The plugin configures your Docker client to talk to Dockhero rather than your default machine. Most of the time you will use 



