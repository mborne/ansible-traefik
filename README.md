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

The whole `/etc/traefik/` directory is watched by traefik. You may add extra config files in `/etc/traefik/conf.d` directory.

See [docs/sample-configs.md](docs/sample-config.md).

## Warning

**Note that security and playbook stability is not guaranteed!**

For example, a dedicated traefik user should be used to run the service (so it might change soon...).

## License

[MIT](LICENSE)
