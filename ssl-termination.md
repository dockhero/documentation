# SSL Endpoints

Sometimes you'll need your microservice to have a valid SSL certificate. For example, if you consume the microservice directly from the front-end, you'll get "Mixed Content" warning or error if your site uses This comes handy when you need to consume the micro-service directly from the front-end.

Each Dockhero cluster comes with two CloudFlare endpoints configured: one in *flexible ssl* mode and another in *full ssl* mode. They have valid SSL certificate installed, so that you don't need to purchase one yourself. Both endpoints are exposed to your Heroku environment:

```bash
$ heroku config:get DOCKHERO_FLEXIBLE_SSL_URL
$ heroku config:get DOCKHERO_FULL_SSL_URL
```

SSL is terminated at the CloudFlare edge server, then the request is sent to Dockhero cluster via http:// or https:// protocol depending on SSL mode (flexible or full).

With Flexible SSL, you don't need to implement SSL in your stack at all.

![Flexible SSL](https://support.cloudflare.com/hc/en-us/article_attachments/206124658/cfssl_flexible.png)

With Full SSL, your stack still needs to talk SSL, but you can use a self-signed certificate. No worries, the users will see a valid CloudFlare's certificate - find more about CloudFlare SSL in [this article](https://support.cloudflare.com/hc/en-us/articles/200170416-What-do-the-SSL-options-mean-)

![Full SSL](https://support.cloudflare.com/hc/en-us/article_attachments/206167937/cfssl_full.png)


If for some reason you prefer SSL termination right within your stack, you can use [Let's Encrypt](https://letsencrypt.org/) to get a self-renewing certificate. See our HTTP/2 + SSL + QUIC proxy tutorial.