# Create LetsEncrypt wildcards certificates with DNS challenge

For `traefik_ssl_cert` and `traefik_ssl_key`, note that the following command allows to generate a LetsEncrypt wildcard certificate for `*.example.net` with a [DNS challenge](https://letsencrypt.org/docs/challenge-types/#dns-01-challenge) :

```bash
sudo certbot certonly --cert-name example.net \
  --server https://acme-v02.api.letsencrypt.org/directory \
  --preferred-challenges dns \
  --manual -d '*.example.net'
```

(See also [lego](https://go-acme.github.io/lego/) to avoid manual registration of a TXT entry on the DNS.)

