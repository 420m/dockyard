Dockyard
========

TL;DR
-----

Each subdirectory contains a docker-compose setup. Setups can be combined, for
instance, you can spawn Traefik to act as a router to server-compents in  other
setups.

## Requirements

NOTE: All the following should be applied on the machine you want to setup our
Plex stack on.

- install Apache `htpasswd`
- install [Docker](https://www.docker.com/)
- install [Docker Compose](https://docs.docker.com/compose/)
- clone this repository in a folder of your choice, where you want all your
  media to be stored
- a domain (or subdomain) name with A records pointing to your server IP
```
# Replace example.com with your (sub)domain here
example.COM       A <YOUR_SERVER_IP>
*.example.com     A <YOUR_SERVER_IP>
```

- Export these env vars in your `.bashrc/.zshrc`:
```shell
export TRAEFIK_ADMIN_PORT=8080
# Change example.com with your domain name
export DOMAIN_NAME=fsociety.tel
# Change me@example.com with your domain name
export ACME_EMAIL=me@example.com
export USER_ID=${UID}
export GROUP_ID=${GID}
```

- then resource .zshrc/.bashrc, or simply log out of your server and connect again
```
# Bash
source ~/.bashrc

# ZSH
source ~/.zshrc
```

- protect your server with authentication (enabled on all services, no need to
  log-in on all of them)
```
# Jump into the repo you just cloned
cd dockyard

htpasswd -c htpasswd <YOUR_USER_NAME_HERE>
# you will then be prompted for your password
# an htaccess file will be created
```


- finally bring up your stack (you can use [ctop](https://ctop.sh) to monitor
  your stack)
```shell
# Bring up the stack !
docker-compose up -d
```

## Configuration

## Plex

Plex won't be opened to the web when you start it for the first time. For that
reason, you'll need to create an SSH tunnel to perform the initial configuration

```shell
ssh -L 32400:127.0.0.1:32400 <YOUR_SERVER>
# Don't close the SSH session or your terminal until you finish the setup
```

Then, you can reach `http://127.0.0.1:32400` in your browser and follow the
instructions. You will then be able to access your Plex server on
[https://app.plex.tv](https://app.plex.tv).

TODO: recommend TLS setup on the Plex server itself

## Transmission

TODO: protect via password using Traefik

## Radarr

TODO: protect via password using Traefik

## Sonarr

TODO: protect via password using Traefik

## Ombi

TODO: protect via password using Traefik

## PlexPy

TODO: protect via password using Traefik

## Jackett

TODO: protect via password using Traefik

## Where to find your media ?

In the `dockyard` (our repo) folder, a `media` subfolder will be created.
This is where all your content will be stored. This is the folder to
backup up and relocate to another server in case you need to migrate your
data from one machine to another.

## Troubleshooting

### Docker-Compose commands

All these commands must be run at the root of the repo you cloned

- getting logs from your container:
```shell
docker-compose logs

# Only logs for a given set of services
docker-compose logs plex proxy
```

### Accessing Traefik's user interface

Traefik's user interface is not exposed publicly. To connect to it, you can use
SSH-tunneling on port `8080`:
```shell
ssh -L 8080:127.0.0.1:8080 <YOUR_SERVER>
# don't close the SSH session
```

The interface will be accessible under `http://localhost:8080` on your local
machine.

## Disclaimer

We can't be held responsible for what you'll do with the setups (don't download
stuff illegally, etc. etc.)

## Maintainers

* [hkaj](/hkaj)
* [elafarge](/elafarge)


