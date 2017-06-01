Dockyard
========

TL;DR
-----

Each subdirectory contains a docker-compose setup. Setups can be combined, for
instance, you can spawn Traefik to act as a router to server-compents in  other
setups.

## Requirements

 * [Docker](https://www.docker.com/community-edition)
 * [Docker-Compose](https://docs.docker.com/compose/install/)

... that's all you should ever need.

## Deploying a setup

Refer to the README in the desired setup subfolder. We'll craft a script that
helps spawning and destroying setups when we get the chance.

### Stable setups

 * [Traefik](./traefik): reverse proxy with automatic TLS (Let's Encrypt), it
   discovers containers and redirects HTTPs requests to their target containers
   based on subdomains or request path prefixes.
 * [Media Server](./media): a Plex-Sonarr-Radarr-Transmission setup to organize
   all your media.

## Disclaimer

We can't be held responsible for what you'll do with the setups (don't download
stuff illegally, etc. etc.)

## Maintainers

* [hkaj](/hkaj)
* [elafarge](/elafarge)


