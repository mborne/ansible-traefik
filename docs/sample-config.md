# Traefik - sample config files

## Define a rateLimit middleware

Use the following `/etc/traefik/conf.d/rate-limit.toml` to get a `test-ratelimit@file` middleware :

```toml
[http.middlewares]
  [http.middlewares.test-ratelimit.rateLimit]
    average = 100
    burst = 50
```

## Configure certificates

Use the following `/etc/traefik/conf.d/rate-limit.toml` to configure certificates generated with [mkcert](https://github.com/FiloSottile/mkcert) :

```toml
# mkcert "*.dev.localhost"
[[tls.certificates]]
    certFile = "/etc/dev-cert/_wildcard.dev.localhost.pem"
    keyFile  = "/etc/dev-cert/_wildcard.dev.localhost-key.pem"

# mkcert "*.example.net"
[[tls.certificates]]
    certFile = "/etc/dev-cert/_wildcard.example.net.pem"
    keyFile  = "/etc/dev-cert/_wildcard.example.net-key.pem"
```

Note that you may also [create LetsEncrypt wildcards certificates with DNS challenge](letsencrypt-wildcard.md).

## Router to external service

Use the following `/etc/traefik/conf.d/jenkins.toml` to expose jenkins running on host :

```toml
[http.services]
  [http.services.jenkins.loadBalancer]
    [[http.services.jenkins.loadBalancer.servers]]
      url = "http://127.0.0.1:8080/"


[http.routers.jenkins]
  rule = "Host(`jenkins.dev.localhost`)"
  service = "jenkins@file"
```
