# media-server
A media server configuration to run Sonarr, Couchpotato and Transmission in Docker, behind Nginx and in connection with Plex.

## Steps
- create a `media` user with a home directory and docker access
- clone this repository in `media`'s $HOME
- run `docker-compose up -d`
- add `/sonarr` to `/home/media/sonarr/config/config.xml` in `UrlBase`
- add `/couchpotato` to `/home/media/couchpotato/config/config.ini` in url_base
- `chown -R 911:911 couchpotato/movies`
- `chown -R 911:911 sonarr/series`
- restart both of them

## Config

### Sonarr
- setup auto-update and authentication
- connect transmission as a downloader
**Caution**: The Host parameter must be the default gateway for the Sonarr container. Bonus: set the `Category` field to Sonarr to make Sonarr use a subfolder and not mix movies with TV shows.

### Couchpotato
- setup auth
- connect transmission as a downloader
**Caution**: The Host parameter must be the default gateway for the Sonarr container.
- configure a ratio limit for seeding

### Nginx
Use media.conf as an example (replace `$YOUR_DOMAIN` with your own domain). It exposes Couchpotato on the `/couchpotato` route, Sonarr on `/sonarr` and transmission on `/transmission/web/`

It also supports SSL that you can setup easily with [letsencrypt](https://letsencrypt.org/). You can comment out the `For HTTPS` part to drop SSL but it's not recommended.


## TODO:
- automate all the things! 

