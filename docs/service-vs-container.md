# Traefik as a service vs traefik as a container?

When traefik is deployed as a service :

* It's easier to whitelist client IPs accessing containers (traefik sees the real client IPs)
* Exposed containers doesn't have to share a docker network with Traefik (the host as access to all running containers)
