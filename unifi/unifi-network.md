---
description: Information relatives à l'installation et l'utilisation de Unifi Network
---

# Unifi Network

## Installation

### Linux (Ubuntu)

Pour faire l'installation de Unifi Network sur Linux, nous allons utilisé le script de "GLENNR".

([https://glennr.nl/s/unifi-network-controller](https://glennr.nl/s/unifi-network-controller))

1. Copiez le lien du script
2. Connectez-vous en SSH sur votre serveur Linux
3. Assurez-vous que le `ca-certificates` package est installé
   1. ```
      sudo apt-get update; sudo apt-get install ca-certificates wget -y
      ```
4. Télécharger le script (Ajusté la version en conséquence)
   1. ```
      wget https://get.glennr.nl/unifi/install/unifi-7.0.25.sh
      ```
5. Exécuter la commande suivante pour démarrer le script
   1. ```
      sudo bash unifi-7.0.25.sh
      ```
6. Une fois l'installation complété, dirigez-vous vers l'adresse de votre serveur
   1. ```
      https://ip.of.your.server:8443
      ```

## Layer 3 Adoption

Il peut arriver pour plusieurs raison que vous ne puissiez adopter un périphérique via l'interface du Unifi Network. Voici une des méthodes disponibles.

### SSH

{% hint style="info" %}
Les identifiants par défaut sont ubnt/ubnt
{% endhint %}

{% hint style="warning" %}
Si vous tentez d'adopter un AP via le contrôleur Unifi version Windows, vous devrez peut-être désactiver votre pare-feu Windows Defender afin de recevoir le "inform"
{% endhint %}

1. Connectez vous en SSH au périphérique que vous tentez d'adopter
2. Utilisez la commande suivante pour annoncer votre périphérique au contrôleur
   1. ```
      set-inform http://ip-of-host:8080/inform
      ```
3. Si vous périphérique était déjà configuré avec un autre contrôleur, vous devez avoir récupéré vos identifiants SSH dans l'ancien contrôleur
   1. Vous pouvez ensuite exécutez la commande suivante pour réinitialiser le périphérique
   2. ```
      sudo syswrapper.sh restore-default
      ```
