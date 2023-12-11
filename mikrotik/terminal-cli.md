---
description: >-
  Documentation en lien avec les différentes commandes utiles dans un terminal
  Mikrotik
---

# Terminal (CLI)

## VPN

### VPN Logging

Commande permettant de montrer toutes les récentes connexion VPN par utilisateur:

```php
/log print where topics=pptp,ppp,info,account
```

## Configuration

### Exportation

Voici une commande permettant d'afficher l'ensemble de la configuration du routeur:

{% hint style="warning" %}
**Attention**: Les mot de passe sont affichés en texte clair
{% endhint %}

```php
/export
```

Il est également possible d'exporter l'ensemble de la configuration vers un fichier avec la commande suivante:

```php
/export file=config
```
