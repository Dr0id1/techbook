---
description: Voici les étapes afin de configurer une sauvegarde avec VCC
---

# 🧾 Configuration sauvegarde (VCC)

## Veeam Agent (Windows 10)

### Ajout licence Cloud Connect

Pour être en mesure de faire une sauvegarde en utilisant la fonction Cloud Connect, il est impératif d'ajouter la licence correspondante. Celle-ci peut être généré à partir du portail Veeam Resseller.

#### Ajout de la licence dans Veeam Agent

Ouvrez le "Control Panel" puis cliquez sur sur "About"

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Puis, téléverser le fichier ".lic" afin d'ajouter la licence dans le module Veeam Agent

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

L'option "Workstation" devrait maintenant être sélectionné

### Backup Job

Une fois le Veeam agent installé, démarrer le puis créer une nouvelle "Backup Job"

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption><p>Fenêtre de création d'une "Backup Job"</p></figcaption></figure>

{% hint style="warning" %}
Nommez selon la manière suivante: Job \<PC/VM> \<Nom Client> - \<Nom Poste>
{% endhint %}

Vous arriverez ensuite au types de sauvegarges. Choissisez "Entire Computer"

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Pour la destination, nous allons sélectionner "Veeam Cloud Connect repository".

{% hint style="warning" %}
Si l'option n'est pas disponible, vérifier que votre licence Veeam Agent est de type "Workstation".
{% endhint %}

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Entrez le DNS

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Entrez les informations de connexion (Créé préalablement dans la section "Tenants" de VCC

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Sélectionner le "Cloud Repositorie" qui a été mis à disposition du "Tenant"

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
"Keep backups for: " **14 jours**
{% endhint %}



Sélectionner l'option "Advanced". Et cochez les options suivantes:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Vous pouvez ensuite vous rendre directement à "Schedule" et remplissez les options tel que vue ci-dessous:

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>
