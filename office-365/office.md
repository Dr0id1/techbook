# 🏢 Office

## Licence

### Clé d'activation

Voici une commande afin de trouver la licence office actuellement installé sur le poste.

{% hint style="warning" %}
Le CMD doit être exécuté en tant qu'administrateur
{% endhint %}

```powershell
cscript "C:\Program Files\Microsoft Office\Office16\OSPP.VBS" /dstatus
```

Si votre version d'office est en 32 bits, utilisez plutôt cette commande:

```sh
cscript "C:\Program Files (x86)\Microsoft Office\Office16\OSPP.VBS" /dstatus
```
