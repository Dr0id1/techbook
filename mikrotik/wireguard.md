---
description: Guide pour configurer WireGuard Road Warrior
---

# 🛡️ WireGuard

## Interface

Il faut débuter avec la création de l'interface WireGuard.&#x20;

Pour ce faire, rendez-vous dans WireGuard -> WireGuard -> +

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption><p>Nommez votre interface</p></figcaption></figure>

{% hint style="warning" %}
Attention que votre port 13231 ne soit pas déjà utilisé par un service (PBX RTP)
{% endhint %}

Une fois appliqué, les clés privées et publiques seront créer automatiquement.

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Vous pouvez changer le port d'écoute par défaut.
{% endhint %}

## Firewall

Nous allons maintenant ajuster le firewall pour permettre les connexions entrantes.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Assurez vous de mettre votre règle dans le bonne ordre.
{% endhint %}

Ajoutez ensuite l'interface WireGuard à votre interface list "LAN". De cette façon, vos clients vpn auront accès au réseau local.

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

## Address

Il faut créer le réseau qui sera utiliser par notre interface WireGuard-Main

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

## Peers

Nous allons configurer notre premier peer.&#x20;

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

**Interface:**  Sélectionner l'interface que nous avons créer dans les étapes précédentes

**Public Key:** Insérer la clée publique fournis par votre client (Windows/Android)

**Private Key:** N/A

**Endpoint:**  N/A (Est utilisé lors de la création d'un STS)

**Endpoint Port:**  N/A (Est utilisé lors de la création d'un STS)

**Allowed Address:** Spécifier à l'aide d'un "/32" l'adresse que vous allez attribuer à votre client. Dans le cas d'un STS, inscrivez les subnets que vous souhaitez autorisé en plus de votre /32.

**Preshared Key:** N/A

**Persistent Keepalive:** Utile pour conserver une connexion active en tout temps (Ex: Site-to-Site)

{% hint style="danger" %}
Attention de ne pas attribuer 2 fois la même adresse.
{% endhint %}

### Client Windows

Nous allons configurer le client Windows. Vous pouvez télécharger l'application WireGuard à l'adresse suivante:

{% embed url="https://download.wireguard.com/windows-client/" %}

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption><p>Voici l'application une fois installé</p></figcaption></figure>

Nous allons ajouté un tunnel vide à l'aide de la flèche.

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Vous devriez obtenir la fenêtre suivante. Copiez la clé publique et coller la dans votre fenêtre peer de l'étape précédente.

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Nous allons utilisé le template suivant pour configurer notre tunnel du côté client.

```wiki
[Interface]
PrivateKey = *CLÉ PRIVÉ GÉNÉRÉ AUTOMATIQUEMENT POUR VOTRE INTERFACE CLIENT*
Address = 192.168.80.5/32
DNS = 192.168.80.1

[Peer]
PublicKey = *CLÉ PUBLIQUE DE VOTRE INTERFACE WIREGUARD SERVEUR*
AllowedIPs = 0.0.0.0/0
Endpoint = *ADRESSE DU SERVEUR WIREGUARD AVEC LE PORT*

```

Vous devriez obtenir le résultat suivant:

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>
