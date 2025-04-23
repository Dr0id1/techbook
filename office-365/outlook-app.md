# 📬 Outlook (App)

## Résolution de problème

### Réparation

Si la réparation conventionnel n'est pas un succès, vous pouvez utiliser l'outil de Microsoft [ici](https://aka.ms/SaRA-officeUninstallFromPC)

### Indexation des courriels

Voici comment reconstruire l'indexation des courriels:

1. Cliquez sur **Fichier**
2. Cliquez sur **Option**
3. Cliquez sur **Recherche** et puis sur **Options d'indexation...**

![](<../.gitbook/assets/image (16).png>)

1. Cliquez sur **Avancé**

![](<../.gitbook/assets/image (32).png>)

1. Cliquez sur **Reconstruire**

![](<../.gitbook/assets/image (44).png>)

### Augmenter la taille  maximale des fichiers PST

La taille par défaut des fichiers PST et OST est de 50 Go mais il y a une valeur de registre qui permet d'augmenter le maximum jusqu'à environ 4 PO (4096 To)

#### Via le registre

Pour augmenter la taille maximale des fichiers pst et ost dans Outlook, vous devrez créer et définir 2 valeurs à l'emplacement suivant dans le registre

* Outlook 2007
  * HKEY\_CURRENT\_USER\Software\Microsoft\Office\11.0\Outlook\PST
* Outlook 2010
  * HKEY\_CURRENT\_USER\Software\Microsoft\Office\14.0\Outlook\PST
* Outlook 2013
  * HKEY\_CURRENT\_USER\Software\Microsoft\Office\15.0\Outlook\PST
* Outlook 2016 / Outlook 2019 / Outlook 2021 / Office 365
  * HKEY\_CURRENT\_USER\Software\Microsoft\Office\16.0\Outlook\PST

Il faut ajouter ces 2 valeurs DWORD

* WarnLargeFileSize
  * `4090445042` (decimal) ou`f3cf3cf2` (hexadecimal)
* MaxLargeFileSize
  * `4294967295` (decimal) ou `ffffffff` (hexadecimal)

![Vous devriez obtenir ce résultat](<../.gitbook/assets/image (3) (1).png>)

#### Via les GPO

Voici le chemin de la GPO

`User Configuration-> Administrative Templates-> Microsoft Outlook`` `_`<version>`_`-> Miscellaneous-> PST Settings.`

Les deux paramètres suivants doivent être modifiés:

* Large PST: Absolute maximum size
  * Don’t set this higher than `4294967295`
* Large PST: Size to disable adding new content
  * Don’t set this higher than `4090445042`

### Migration de IMAP vers Exchange

#### Script VBS

Il est possible que suite à une migration de courriel IMAP vers Exchange, que les courriels et les sous-dossier ne soit plus visible.

Il existe un script VBS qui permet de modifié la propriété de chaque dosser afin de les convertis au mode "IPF.Note".

Une fois le script téléchargé, exécutez le et ouvrez Outlook.

{% @github-files/github-code-block url="https://github.com/Dr0id1/Playbooks/blob/master/VBS/FixImportedIMAPFolders.vbs" %}

#### Manuellement

Il est également possible de le faire manuellement à l'aide de l'outil MFCMAP que vous pouvez téléchargez [ici](https://github.com/microsoft/mfcmapi/releases).

Exécutez le et connectez-vous

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

Sélectionnez le profil

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

Double-Cliquez sur la boite courriel concerné

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

Ouvrez le conteneur racine puis ouvrez "IPM\_SUBTREE"

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Sélectionnez un conteneur IMAP et modifiez la propriété "PR\_CONTAINER\_CLASS"

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

Remplacez "IPF.Imap" par "IPF.Note"

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Cliquez sur "OK" et répétez ces étapes pour tout les dossiers et sous-dossiers conercnés.
