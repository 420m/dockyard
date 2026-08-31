# Media Server

A media server configuration to run Jellyfin, Sonarr, Radarr, and qbittorrent in Docker and behind Traefik.

## First run

- install [Docker](https://www.docker.com/)
- install [Docker Compose](https://docs.docker.com/compose/)
- clone this repository
- create a `web` docker network with `docker network create web`
- clone and setup [the reverse proxy](https://github.com/hkaj/reverse_proxy)
- create a user for your media server, export its `$USER_ID` and `$GROUP_ID`.
- if there's a mounted SMB volume, make that user part of the group that has permissions to write in it
- set your TZ as an env var, using this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List), e.g. "Europe/Paris"
- create a folder named `media` in this folder (`dockyard`) owned by $USER_ID:$GROUP_ID from your `media` user.
- if you want to setup a VPN or SOCKS5 proxy to secure qbittorrent traffic, do that and uncomment the corresponding env var in the qbittorrent service
- run `DOMAIN_NAME="..." USER_ID="$USER_ID" GROUP_ID="$GROUP_ID" TZ="$TZ" docker compose up -d`
- profit :)

## Config

The expected folder structure is:

```
media/
  library/  # where jellyfin will look, and where sonarr/radarr will hardlink to
    movies/
    tv/
  torrents/  # where qbittorrent will download content and where sonarr/radarr will hardlink from
    movies/
    tv/
```

* Configure qbittorrent to download torrents
    * To connect to it, check its container logs. It generates a random password upon each start.
* Create a movies and a tv categories in qbittorent
* Configure a download client in sonarr and radarr to use qbittorrent, pass them the above mentioned categories
* Configure indexers in prowlarr
* Configure prowlarr to connect to sonarr and radarr
* Configure Sonarr and Radarr to use hardlinking and avoid copying files in `Settings => Media Management => Importing`
* In Jellyfin, add the opensubtitles plugin
