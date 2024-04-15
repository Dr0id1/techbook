---
description: Notes pour Traefik et Cloudflare
---

# 🛣️ Traefik / CloudFlare

## Traefik&#x20;

### Fichier de config YML

```yaml
  insecure: true  # Don't do this in production!

# Entry Points configuration
# ---
entryPoints:
  web:
    address: :80
    # (Optional) Redirect to HTTPS
    # ---
     http:
       redirections:
         entryPoint:
           to: websecure
           scheme: https

  websecure:
    address: :443

 certificatesResolvers:
#   staging:
#     acme:
#       email: your-email@example.com
#       storage: /etc/traefik/certs/acme.json
#       caServer: "https://acme-staging-v02.api.letsencrypt.org/directory"
#       httpChallenge:
#         entryPoint: web
#
   production:
     acme:
       email: admin@wickedgroup.ca
       storage: acme.json
       caServer: "https://acme-v02.api.letsencrypt.org/directory"
       httpChallenge:
         entryPoint: websecure

# (Optional) Overwrite Default Certificates
# tls:
#   stores:
#     default:
#       defaultCertificate:
#         certFile: /etc/traefik/certs/cert.pem
#         keyFile: /etc/traefik/certs/cert-key.pem
# (Optional) Disable TLS version 1.0 and 1.1
#   options:
#     default:
#       minVersion: VersionTLS12

providers:
  docker:
    exposedByDefault: false  # Default is true
  file:
    # watch for dynamic configuration changes
    directory: /etc/traefik
    watch: true

```

### Docker-Compose

```yaml
version: '3'

services:
  reverse-proxy:
    # The official v2 Traefik docker image
    image: traefik:v2.7
    # Enables the web UI and tells Traefik to listen to docker
    command:
      - "--entrypoints.websecure.address=:443"
      - "--api.insecure=true"
      - "--providers.docker"
      - --certificatesresolvers.myresolver.acme.email=admin@wickedgroup.ca
      - --certificatesresolvers.myresolver.acme.storage=/etc/traefik/acme.json
      - --certificatesresolvers.myresolver.acme.tlschallenge=true
     #- "--providers.docker.exposedbydefault=false"

    ports:
      # The HTTPs port
      - "443:443"
      # The Web UI (enabled by --api.insecure=true)
      - "8484:8080"
    volumes:
      # So that Traefik can listen to the Docker events
      - /var/run/docker.sock:/var/run/docker.sock
      #- ~/Traefik/acme.json:/etc/traefik/acme.json
      - ~/Traefik/certs:/etc/traefik/certs
      # - traefik-ssl-certs:/ssl-certs
```

### Containers Labels

Voici les labels à définir dans les conteneurs qui seront aiguiller par Traefik.

<table><thead><tr><th>Labels</th><th>Values</th><th data-hidden></th></tr></thead><tbody><tr><td>traefik.enable</td><td>true</td><td></td></tr><tr><td>traefik.http.routers.sonarr.entrypoints</td><td>websecure</td><td></td></tr><tr><td>traefik.http.routers.sonarr.rule</td><td>Host(`<code>sonarr.wickedbarn.com</code>`)</td><td></td></tr><tr><td>traefik.http.routers.sonarr.tls</td><td>true</td><td></td></tr><tr><td>traefik.http.routers.sonarr.tls.certresolver</td><td>myresolver</td><td></td></tr></tbody></table>

## CloudFlare

![Mettre le mode d'encryption à "Full (strict)"](<../.gitbook/assets/image (2).png>)

![Activer "Always Use HTTP"](<../.gitbook/assets/image (45).png>)

![Activer "Automatic HTTPS Rewrites"](<../.gitbook/assets/image (40).png>)

Il faut maintenant créer une règle qui va venir renforcer le HTTPS Rewrite.

![Remplissez la règle de cette facon](<../.gitbook/assets/image (17).png>)

{% hint style="warning" %}
Assurez-vous d'écrire l'URL en HTTP et non en HTTPS
{% endhint %}

![Voici vos entrés DNS](<../.gitbook/assets/image (27).png>)

{% hint style="warning" %}
Désactiver temporairement le proxy afin de recevoir votre certificat. Une fois le certificat émis, vous pourrez réactiver le proxy.
{% endhint %}
