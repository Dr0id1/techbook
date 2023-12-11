---
description: Voici comment configurer un trunk VOIP.ms sur FreePBX (SIP et PjSIP)
---

# Configuration

## Connectivity

### Trunk (SIP)

Voici un exemple de configuration pour un Trunk (SIP Legacy)

#### CID

"Mon Entreprise" <5145551234>

#### Dial Number Manipulation Rules

> 1NXXNXXXXXX
>
> NXXNXXXXXX
>
> 911

#### Outgoing

Trunk Name: _179507\_subaccount_

```
username=179507_subaccount
type=peer
trustrpid=yes
sendrpid=yes
secret=motdepassesip
qualify=yes
nat=yes
insecure=invite
host=montreal5.voip.ms
fromuser=179507_subaccount
disallow=all
context=from-trunk
canreinvite=nonat
allow=ulaw
```

#### Incoming

```
179507_subaccount:motdepassesip@montreal5.voip.ms:5060
```

### Trunk (PJSIP)

#### General

Les informations de bases doivent être saisie de la manière suivante:

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

#### Advanced

Complété les champs suivants:

* From Domain
* From User
*
