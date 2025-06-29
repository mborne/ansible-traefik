# ansible-traefik

Ansible playbook to deploy [Traefik](https://doc.traefik.io/traefik/) as a systemd service **for a DEV usage**.

## Description

* Download binary from [github releases](https://github.com/traefik/traefik/tags) (`/opt/traefik/traefik`)
* Create a traefik group and a traefik user
* Create a systemd service (`/etc/systemd/system/traefik.service`)
* Configure traefik focussing on the exposition of docker containers running on a single host (`/etc/traefik/traefik.toml`)

## Parameters

See comments in [defaults/main.yml](defaults/main.yml) and [templates/etc/traefik/traefik.toml.j2](templates/etc/traefik/traefik.toml.j2)

## Warning

**Note that security and playbook stability is not guaranteed!**

For example, a dedicated traefik user should be used to run the service (so it might change soon...).

## Notes

* [Traefik as a service vs traefik as a container](docs/service-vs-container.md)
* [Traefik - Sample additional config files](docs/sample-config.md)
* [Troubleshooting - Failed to allocate directory watch: Too many open files](docs/too-many-open-files.md)

## License

[MIT](LICENSE)
