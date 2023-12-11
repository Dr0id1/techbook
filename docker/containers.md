# Containers

## Docker Run

{% hint style="warning" %}
Les commandes suivantes, doivent être exécutés en "sudoer"
{% endhint %}

### qBittorrent

```bash
docker create \
  --name=qbittorrent \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -e UMASK_SET=022 \
  -e WEBUI_PORT=8080 \
  -p 6881:6881 \
  -p 6881:6881/udp \
  -p 8080:8080 \
  -v /opt/qbitorrent:/config \
  -v /opt/qbitorrent:/downloads \
  -v /media/share/SeedBox:/SeedBox \
  --restart unless-stopped \
  ghcr.io/linuxserver/qbittorrent
```

### Sonarr

```bash
docker create \
  --name=sonarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America\Montreal \
  -p 8989:8989 \
  -v /opt/sonarr:/config \
  -v /media/share/Séries:/Séries \
  -v /media/share/SeedBox:/SeedBox \
  --restart unless-stopped \
  linuxserver/sonarr
```

### Unifi Controler

```bash
docker create \
  --name=unifi-controller \
  -e PUID=1000 \
  -e PGID=1000 \
  -p 3478:3478/udp \
  -p 10001:10001/udp \
  -p 8080:8080 \
  -p 8081:8081 \
  -p 8443:8443 \
  -p 8843:8843 \
  -p 8880:8880 \
  -p 6789:6789 \
  -v /opt/unifi:/config \
  --restart unless-stopped \
  ghcr.io/linuxserver/unifi-controller
```

### Jackett

```bash
docker create \
  --name=jackett \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Toronto \
  -p 9117:9117 \
  -v /opt/jackett:/config \
  -v /opt/jackett:/downloads \
  --restart unless-stopped \
  linuxserver/jackett
```

### Radarr

```bash
docker create \
  --name=radarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -p 7878:7878 \
  -v /opt/radarr:/config \
  -v /media/share/Films:/movies \
  -v /media/share/SeedBox:/SeedBox \
  -v /opt/radarr/downloads:/downloads \
  --restart unless-stopped \
  linuxserver/radarr
```

### Tautulli

```bash
docker run -d \
  --name=tautulli \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -p 8181:8181 \
  -v /opt/tautulli:/config \
  -v <path to plex logs>:/logs \ # Add path to plex's logs
  --restart unless-stopped \
  ghcr.io/linuxserver/tautulli
```

### FlareSolverr

```bash
docker run -d \
  --name=flaresolverr \
  -p 8191:8191 \
  -e LOG_LEVEL=info \
  -e CAPTCHA_SOLVER=hcaptcha-solver \
  --restart unless-stopped \
  ghcr.io/flaresolverr/flaresolverr:latest
```

### Prowlarr

```shell
sudo docker run -d \
  --name=prowlarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -p 9696:9696 \
  -v /opt/prowlarr:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/prowlarr:develop
```

### Overseerr

```shell
sudo docker run -d \
  --name=overseerr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -p 443:5055 \
  -v /opt/overseerr/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/overseerr:latest
```

### TubeSync

```shell
sudo docker run -d \
  --name tubesync \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -v /opt/tubesync-config:/config \
  -v /media/share/YoutubeSync:/downloads \
  -p 4848:4848 \
  ghcr.io/meeb/tubesync:latest
```

### Lidarr

```shell
sudo docker run -d \
  --name=lidarr \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Montreal \
  -p 8686:8686 \
  -v /opt/lidarr/config:/config \
  -v /media/share/Music:/music  \
  -v /media/share/SeedBox:/SeedBox  \
  --restart unless-stopped \
  lscr.io/linuxserver/lidarr:latest
```

## Docker-Compose

### oznu/cloudflare-ddns

```yaml
version: '2'
services:
  cloudflare-ddns:
    image: oznu/cloudflare-ddns:latest
    restart: always
    environment:
      - API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
      - ZONE=example.com
      - SUBDOMAIN=mysubdomain
      - PROXIED=true
```

### Portainer

```yaml
version: '3'
services:
  portainer:
    image: portainer/portainer-ce:alpine
    container_name: portainer
    command: -H unix:///var/run/docker.sock
    ports:
      - "9000:9000"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "portainer_data:/data"
    restart: always
```
