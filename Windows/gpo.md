# GPO - Group Policy Object

*Permet d'automatiser une floppée de choses dans un domain. Concerne soit à un objet user, soit à un objet computer. S'applique soit sur un domain, soit sur une OU (Organisational Unit). Parallèle avec le CSS pour l'ordre d'application.*

## Application des GPO

Une GPO s'applique sur un Computeur / User :
1. Au start-up / log on
2. Après 180 minutes
3. Avec `gpudpate` 

## Listes de GPO

Console de management : `gpmc`

* **Firewall Off (ancienne version)** : Computer > Policies > Administrative Template > Network > Network Connection > Firewall > Domain > Protet All Network Connection *disabled*
* **Firewall Off (nouvelle version, Win >= 7)** : Computer > Policies > Windows Settings > Security Settings > Windows Firewall...
* **Firewall Services automatic** : Computer > Policies > Windows Settings > System Services - Windows Firewall
* **Do not display later user name** :
* **Do not require CTRL+ALT+DEL** :
* **Block management console** :
* **Acces au control panel** :
* **Snap-ins** :
* **Interdire notre machine d'afficher l'écran de log on, tant que la machine n'a pas lu le SYSVOL. Si la machine boot trop vite et n'a pas le temps de lire le SYSVOL, donc pas lu les GPOs. Attention pour les notebook**
* **Registery | regedit.exe** : (running silently : permet de toujours faire passer un .reg)
* **Vue Standard dans les console de management** :
* **Désactiver compte guest** : Computer > Policies > Windows Settings > Security Settings > Local Policies > Security Options - Accounts: Guest account status
* **Rename guest compte (BrolCourt)** : Computer > Policies > Windows Settings > Security Settings > Local Policies > Security Options - Accounts: Rename guest account
* **Mot de passe guest (BrolCourt1234 : le même sur tous les pc)** : Computer > Preferences > Control Panel Settings > Local Users and Groups - New Local User (je peux aussi le renomer et le désactiver par ici) (Utiliser Windows Enabler pour dégriser la case password)
* **

## Scripts

### Changer le mot de passe du compte guest

```cmd
net user BrolCourt BrolCourt1234
```

Copier GuestPwd.cmd du bureau dans le dossier des scripts de la GPO (C:\Windows\SYSVOL\sysvol\salle403.local\...), applicable dans Computer > Windows Settings > Scripts > Startup/Shutdown ou User > Policies > Windows Settings > Scripts > Logon/Logoff
