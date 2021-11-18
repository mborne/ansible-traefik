# ansible-traefik

Ansible playbook to deploy [traefik](https://doc.traefik.io/traefik/) as a systemd service **for a DEV usage**.

## Description

* Download traefik binary from [github releases](https://github.com/traefik/traefik/tags) (`/opt/traefik/traefik`)
* Create a systemd service (`/etc/systemd/system/traefik.service`)
* Configure traefik focussing on the exposition of docker containers running on a single host (`/etc/traefik/traefik.toml`)


## Parameters

See comments in [defaults/main.yml](defaults/main.yml) and [templates/etc/traefik/traefik.toml.j2](templates/etc/traefik/traefik.toml.j2)

## Notes

### traefik as a service vs traefik as a container?

When traefik is deployed as a service :

* It's easier to whitelist client IPs accessing containers (traefik sees the real client IPs)
* Exposed containers doesn't have to share a docker network with traefik (the host as access to all running containers)

### Additional configs

The whole `/etc/traefik/` directory is watched by traefik. You may add config files like `/etc/traefik/rate-limit.toml` :

```toml
[http.middlewares]
  [http.middlewares.test-ratelimit.rateLimit]
    average = 100
    burst = 50
```

### LetsEncrypt wildcards with DNS

For `traefik_ssl_cert` and `traefik_ssl_key`, note that the following command allows to generate a LetsEncrypt wildcard certificate for `*.example.net` with a [DNS challenge](https://letsencrypt.org/docs/challenge-types/#dns-01-challenge) :

```bash
sudo certbot certonly --cert-name example.net \
  --server https://acme-v02.api.letsencrypt.org/directory \
  --preferred-challenges dns \
  --manual -d '*.example.net'
```

(See also [lego](https://go-acme.github.io/lego/) to avoid manual registration of a TXT entry on the DNS.)

## Warning

**Note that security and playbook stability is not guaranteed!**

For example, a dedicated traefik user should be used to run the service (so it might change soon...).

## License

[MIT](LICENSE)
