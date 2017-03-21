# Media Server

A media server configuration to run Plex, Sonarr, Couchpotato and Transmission in Docker and behind Traefik.


## First run

- clone this repository
- clone and setup [the reverse proxy](https://github.com/hkaj/reverse_proxy)
- create a user for your media server, export its `$USER_ID` and `$GROUP_ID`.
- create a media folder in docker-compose's folder with $USER_ID:$GROUP_ID ownership
- get your Plex claim token at https://www.plex.tv/claim/
- run `DOMAIN_NAME="..." PLEX_TOKEN="..." IP_ADDRESS="..." USER_ID="$USER_ID" GROUP_ID="$GROUP_ID" docker-compose up -d`


## Config


### Transmission

We use [Transmission](https://transmissionbt.com/) as the downloader.

- stop transmission's container
- configure basic auth at `media/transmission/config/settings.json` (you will need to touch `rpc-authentication-required`, `rpc-username` and `rpc-password`)
- start transmission's container


### Sonarr

We use [Sonarr](https://sonarr.tv/) to track and manage TV shows.

- setup auto-update and authentication
- connect transmission as a downloader


### Couchpotato

We use [Couchpotato](https://couchpota.to/) to track and manage movies.

- setup authentication
- connect transmission as a downloader
- configure a ratio limit for seeding


### Jackett

We use [Jackett](https://github.com/Jackett/Jackett) as a proxy between private trackers and our other components.


### Use T411 (French) without Jackett

`docker-compose.yaml` contains a commented-out section about T411-Torznab. Clone [the t411-torznab repo](https://github.com/KiLMaN/T411-Torznab), uncomment this section and add `T411USERNAME` and `T411PASSWORD` environment variables to the startup command to start torznab, which you can use as a proxy to use t411 in Sonarr and Couchpotato.
