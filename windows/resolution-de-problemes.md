---
description: >-
  Cet article contient divers trucs et astuces afin de résoudre certain problème
  en lien avec les différentes version de Windows
---

# Résolution de problèmes

## Windows 7

### Media Creation Tool

#### Erreur 0x80072F8F – 0x20000

Activer TLS 1.1 et TLS 1.2 via le registre

1. Assurez vous que votre système est entièrement mis à jour.
2. Ouvrez le bloc note
3. Copier les lignes suivantes

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp]
"DefaultSecureProtocols"=dword:00000a00

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp]
"DefaultSecureProtocols"=dword:00000a00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"DisabledByDefault"=dword:00000000
"Enabled"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]
"DisabledByDefault"=dword:00000000
"Enabled"=dword:00000001
```

1. Enregistrez le fichier avec une extension .reg - par exemple, enable\_tls.reg
2. Double-cliquez sur le fichier enable\_tls.reg pour appliquer les paramètres dans le registre. Cliquez sur Oui lorsque vous êtes invité à confirmer.
3. Essayez de redémarrer le Windows Media Creation Tool
