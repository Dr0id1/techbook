---
description: Cette page fournie divers trucs et astuces concernant Exchange Online
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# ✉️ Exchange

## Mail Flow

### Courriel Externe

Il est possible de créer une bannière "Avertissement" dans chaque courriel entrant afin de prévenir l'utilisateur que son contenu pourrait être frauduleux. En voici un exemple:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

1. Connectez vous dans la console d'administration Exchange.
2. Ouvrez "**Mail Flow**"
3. Sélectionnez "**Rules**"
4. Créer une nouvelle règle à l'aide du "**+**"

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

1. Donnez un nom à votre règle (Ex: "**External Email Warning**")
2. Cliquez sur "**Apply this rule if**"
   1. Sélectionnez "**The Sender is located...**"
   2. Sélectionnez "**Outside the organization**"

Vous devriez obtenir le résultat suivant:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Nous devons maintenant ajouter la bannière au format HTML:

```html
<!-- Yellow caution banner -->
<table border=0 cellspacing=0 cellpadding=0 align="left" width="100%">
  <tr>
    <!-- Remove the next line if you don't want the Yellow bar on the left side -->
    <td style="background:#ffb900;padding:5pt 2pt 5pt 2pt"></td>

    <td width="100%" cellpadding="7px 6px 7px 15px" style="background:#fff8e5;padding:5pt 4pt 5pt 12pt;word-wrap:break-word">
      <div style="color:#222222;">
        <span style="color:#222; font-weight:bold;">ATTENTION:</span>
        Cet e-mail provient de l'externe. Ne cliquez pas sur les liens ou n'ouvrez pas les pièces jointes à moins de reconnaître l'expéditeur et de savoir que le contenu est sûr.
      </div>
    </td>
  </tr>
</table>
<br />
```

1. Cliquez sur "**Do the following**"
   1. Sélectionner "**Apply a disclaimer to the message"**
   2. Sélectionner "**Prepend the disclaimer**"
   3. Cliquez sur "**Enter text...**"
   4. Collez le code HTML ci-dessus
   5. Cliquez sur "**Select one...**" et cliquez sur "**Wrap**"

Vous devriez obtenir le résultat suivant:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Par la suite, il vous est possible de faire des exceptions pour certain domaine digne de confiance via l'option "**Except if...**".&#x20;

Vous pouvez cliquez sur "**Next**". Vous pouvez ignore les paramètres qui suivent et cliquez encore une fois sur "**Next**" puis sur "**Finish**".

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
N'oubliez pas d'activer votre règle. Autrement elle ne fonctionnera pas.
{% endhint %}

### Courriel Externe - Pieces Jointes

Il est également possible d'ajouter un avertissement supplémentaire en cas de pièces jointes spécifiques. Les étapes sont similaires.

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

```html
<!-- Yellow caution banner -->
<table border=0 cellspacing=0 cellpadding=0 align="left" width="100%">
  <tr>
    <!-- Remove the next line if you don't want the Yellow bar on the left side -->
    <td style="background:#FF0000;padding:5pt 2pt 5pt 2pt"></td>

    <td width="100%" cellpadding="7px 6px 7px 15px" style="background:#FA9191;padding:5pt 4pt 5pt 12pt;word-wrap:break-word">
      <div style="color:#222222;">
        <span style="color:#222; font-weight:bold;">ATTENTION:</span>
        Ce courriel contient un fichier qui pourrait contenir un virus. Dans le doute, ne l'ouvrez pas.
      </div>
    </td>
  </tr>
</table>
<br />
```

## Archivage

Plusieurs éléments sont essentiels pour activer l'archivage d'une boite courriel pour un utilisateur.

### Exchange Admin Console

Premièrement, il faut activer l'archivage pour la boite courriel en question. Sélectionner l'utilisateur et rendez vous dans la section "More Actions"

{% hint style="info" %}
Exchange Admin Console est régulièrement référé par le nom **EAC**
{% endhint %}

!["More Actions" dans la section droite du EAC](<../.gitbook/assets/image (49).png>)

Dans la section de droite, un autre panneau apparaitra avec l'option d'activer l'archivage pour cette boîte courriel.

![On peut également y voir l'espace disponible.](<../.gitbook/assets/image (37).png>)

### Classic Exchange Admin Console

Pour l'instant, les _tags_ qui nous intéressent sont introuvable dans la nouvelle interface Microsoft 365 Compliance. Nous allons donc utiliser la version "Classique" du panneau d'administration Exchange.

Pour ce faire, cliquez sur _Classic Exchange admin center_ dans le coin inférieur gauche.

![Page d'accueil du "Classic Exchange admin center"](<../.gitbook/assets/image (39).png>)

Une fois sur cette page, cliquez sur "Compliance management" puis sur _Retention Tags_. Vous trouverez des "tags" déjà disponible par défaut. Sinon, il est possible d'en créer un qui répond à vos besoins.

![Voici un exemple des tags pouvant déjà être présent](<../.gitbook/assets/image (18).png>)

{% hint style="info" %}
_Default_ représente l'ensemble des boites courriels
{% endhint %}

Une fois que vous avez modifié ou créé le tags dont vous avez besoin, il faut ce rendre à _Retention Policies_.

![Voici une Retention Policies créé manuellement](<../.gitbook/assets/image (4).png>)

Une _Retention Policies_ contient un ou plusieurs _Tags_ que vous pourrez ensuite attribué à une boite courriel.

![Seul un tag est assigné à cet policy](<../.gitbook/assets/image (51).png>)

Pour terminer, il reste à assigner cette _policy_ à une boite courriel. Pour ce faire, cliquez sur _recipients_, sélectionné la boite courriel, éditez-le, et dans _mailbox features_ sélectionnez la _retention policy_ désiré.

{% hint style="warning" %}
Pour mettre à jour immédiatement votre nouvelle règle de rétention, rendez-vous à l'article [Managed Folder Assitant](https://dr0id.gitbook.io/pcsupreme/office-365/exchange-online#managed-folder-assistant).
{% endhint %}

## PowerShell

### Connexion via PowerShell

Tout d'abord, il faut établir la connexion avec l'organisation Office 365. Pour ce faire, ouvrez un PowerShell en mode administrateur.

{% hint style="warning" %}
**Le module suivant est nécessaire pour que les commandes qui suivent fonctionnent.**
{% endhint %}

```
Install-Module -Name ExchangeOnlineManagement
```

```
Import-Module ExchangeOnlineManagement
```

Ensuite, il faut établir la connexion via la commande suivante:

```
Connect-ExchangeOnline -UserPrincipalName admin@pcsupreme.com -DelegatedOrganization pcsupreme.onmicrosoft.com
```

{% hint style="warning" %}
Assurez-vous de remplacer "pcsupreme" par l'organisation à laquelle vous souhaitez vous connecter.
{% endhint %}

Une fenêtre Microsoft apparaitra afin que vous saisissiez le mot de passe du compte que vous avez mentionné ci-dessus. Une fois le mot de passe saisi, la connexion à l'organisation va s'établir (+/- 30 secondes).

### Duplicata courriel

Dans le cas ou nous avons deux courriel ayant le même préfix ( info@domaineA.com et info@domaineB.com), ceci entrainera plusieurs erreurs diverse.

Voici un exemple du code d'erreur renvoyé par Exchange:

```
Error executing request. The proxy address "SMTP:info@pcsupreme.com" is already being used by the proxy addresses or LegacyExchangeDN. Please choose another proxy address.
```

Par exemple, si nous voulons créer une 3e adresse courriel ayant le préfix "info", il faudra créer cette adresse via PowerShell.

### Création d'une boite courriel

Voici la commande afin de créer une 2e adresse courriel ayant le même préfix qu'une autre adresse.&#x20;

{% hint style="warning" %}
**Attention** : les deux adresse doivent être sur deux domaine différent.
{% endhint %}

```bash
New-Mailbox -Name "Info X" -Alias info_X -Shared -PrimarySMTPAddress info@pcsupreme2.com
Name Alias ServerName ProhibitSendQuota
```

Ensuite, vérifier que la boite courriel a bien été créé à l'aide de la commande suivante:

```bash
get-mailbox info_X | select userprincipalname
UserPrincipalName
```

Il faut maintenant assigné le bon nom d'authentification.

```bash
set-mailbox info_X -MicrosoftOnlineServicesID info@pcsupreme2.com
```

### SMTP AUTH

Si nous souhaitons activé le SMTP AUTH et que encore là nous avons deux adresses ayant le même préfix, il nous faudra opter pour PowerShell afin d'activer cette fonction. Voici la commande à utiliser:

```bash
Set-CASMailbox -Identity info@pcsupreme.com -SmtpClientAuthenticationDisabled $false
```

Et l'inverse, pour la désactiver.

```bash
Set-CASMailbox -Identity info@pcsupreme.com -SmtpClientAuthenticationDisabled $true
```

Ces deux commande sont également valables dans n'importe quel autre scénario ou le panneau d'administration ne nous permettrais pas d'activer cette fonction.

### Managed Folder Assistant

Cet outil permet d'appliquer immédiatement les nouvelles règles de rétention (Rétention + Archive). Autrement, les règles peuvent prendre jusqu'à 7 jours pour être mise à jour. Une fois [connecté](https://app.gitbook.com/@dr0id/s/pcsupreme/\~/drafts/-MjjBc9AQf2FE213V7eQ/office-365/exchange-online#connexion-via-powershell), vous pouvez exécuter ces commandes:

```bash
$Mailboxes = Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"}
```

```powershell
$Mailboxes.Identity | Start-ManagedFolderAssistant
```

### Changer la langue d'une boite courriel

La commande suivante permet de changer la langue des dossiers par défaut d'une boite courriel

{% hint style="info" %}
L'adresse courriel est aussi valide comme "Identity"
{% endhint %}

```powershell
Set-MailboxRegionalConfiguration -Identity "Prénom Nom" -Language fr-ca -LocalizeDefaultFolderName
Set-MailboxRegionalConfiguration -Identity "Prénom Nom" -Language en-ca -LocalizeDefaultFolderName
```

Il est également possible de changer pour tout les utilisateurs en utilisant la commande suivante:

```powershell
Get-Mailbox -ResultSize Unlimited | Set-MailboxRegionalConfiguration -Language fr-ca -LocalizeDefaultFolderName
```
