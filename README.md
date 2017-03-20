# media-server

A media server configuration to run Plex, Sonarr, Couchpotato and Transmission in Docker and behind Traefik.


## First run

- clone this repository
- clone and setup [the reverse proxy](https://github.com/hkaj/reverse_proxy)
- get your Plex claim token at https://www.plex.tv/claim/
- run `DOMAIN_NAME=... PLEX_TOKEN="..." IP_ADDRESS="..." docker-compose up -d`


## Config


### Transmission

- stop transmission's container
- configure basic auth at `media/transmission/config/settings.json` (you will need to touch `rpc-authentication-required`, `rpc-username` and `rpc-password`)
- start transmission's container


### Sonarr

- setup auto-update and authentication
- connect transmission as a downloader
**Caution**: The Host parameter must be the default gateway for the Sonarr container. Bonus: set the `Category` field to Sonarr to make Sonarr use a subfolder and not mix movies with TV shows.


### Couchpotato

- setup auth
- connect transmission as a downloader
**Caution**: The Host parameter must be the default gateway for the Sonarr container.
- configure a ratio limit for seeding


### Use T411 (French)

`docker-compose.yaml` contains a commented-out section about torznab. Clone torznab from GitHub, build the image, uncomment this section and add `T411_USER` and `T411_PASS` environment variables to the startup command to start torznab, which you can use as a proxy to use t411 in Sonarr and Couchpotato.


## TODO:

- setup auto letsencrypt
- figure out permissions on `media`
- provide default config
