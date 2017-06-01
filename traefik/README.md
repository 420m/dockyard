# Traefik: a TLS-enabled reverse-proxy integrated with Docker

Traefik automatically routes requests to container in other setups. To launch
it, simply run

```shell
ADMIN_PORT="8080" DOCKER_DOMAIN="YOUR_DOMAIN_NAME" ACME_EMAIL="you@example.com" docker-compose up -d
```
