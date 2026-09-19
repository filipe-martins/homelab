version: '3.8'

services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    user: 1000:1000
    network_mode: "host"
    volumes:
      - ./jellyfin/config:/config
      - ./jellyfin/cache:/cache
      - /mnt/media/filmes:/data/filmes
      - /mnt/media/series:/data/series
    restart: unless-stopped

  navidrome:
    image: deluan/navidrome:latest
    container_name: navidrome
    user: 1000:1000
    ports:
      - "4533:4533"
    environment:
      ND_SCANSCHEDULE: 1h
      ND_LOGLEVEL: info
      ND_BASEURL: ""
    volumes:
      - ./navidrome/data:/data
      - /mnt/media/musica:/music:ro
    restart: unless-stopped

  freshrss:
    image: freshrss/freshrss:latest
    container_name: freshrss
    ports:
      - "8080:80"
    environment:
      TZ: 'Europe/Lisbon'
      CRON_MIN: '1,31'
    volumes:
      - ./freshrss/data:/var/www/FreshRSS/data
    restart: unless-stopped

  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      PUID: 1000
      PGID: 1000
      TZ: Europe/Lisbon
    volumes:
      - ./sonarr/config:/config
      - /mnt/media/series:/tv
    ports:
      - 8989:8989
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      PUID: 1000
      PGID: 1000
      TZ: Europe/Lisbon
    volumes:
      - ./radarr/config:/config
      - /mnt/media/filmes:/movies
    ports:
      - 7878:7878
    restart: unless-stopped

  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    environment:
      PUID: 1000
      PGID: 1000
      TZ: Europe/Lisbon
    volumes:
      - ./bazarr/config:/config
      - /mnt/media/filmes:/movies
      - /mnt/media/series:/tv
    ports:
      - 6767:6767
    restart: unless-stopped