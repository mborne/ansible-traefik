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

```yaml
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

