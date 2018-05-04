# GPO - Group Policy Object

*Permet d'automatiser une floppée de choses dans un domain. Concerne soit à un objet user, soit à un objet computer. S'applique soit sur un domain, soit sur une OU (Organisational Unit). Parallèle avec le CSS pour l'ordre d'application.*

## Application des GPO

Une GPO s'applique sur un Computeur / User :
1. Au start-up / log on
2. Après 180 minutes (300 secondes pour un DC)
3. Avec `gpudpate` 

## Status GPO

Dans le détail d'un GPO, je peux modifier son status et lui demander de désactiver les clés Users ou Computers si ma GPO n'a que des clés Computers ou Users.

## Ajouter de nouvelles GPOs

### ADM

1. Copier le .admx dans C:\Windows\PolicyDefinitions et le .adml dans C:\Windows\PolicyDefinitions\en-US\

### Ajouter les Windows 10 Fall Creators Update

1. Télécharger le .msi, l'exécuter et trouver le dossier PolicyDefinitions dans C:\Program Files (x86)\Microsoft Group Policy\Windows 10 Fall Creators Update (1709)
2. Copier PolicyDefinitions dans C:\Windows\SYSVOL\sysvol\salle403.local\Policies\
3. Copier PolicyDefinitions à la place du dossier qui existe déjà dans C:\Windows\ (remplacer et skip)

## Listes de clés GPO

#### Attention, si on change le status d'un service en automatique, son status se mettra à jour comme avec n'importe quelle règle MAIS la machine doit redémarrer pour que le service démarre.

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
* **Pareil pour admin, attention au compte admin du domain !** Password = MdP1234
* **Préférences affichage fenêtre** : Users > Preferences > Control Panel Settings > Folder Options > New (at least Win Vista)
* **Bloquer les comptes microsoft** :
* **Ne pas afficher les infos utilisateurs à l'écran verrouiller** : Computer > Policies > Windows Settings > Security Settings > Security Options - Interactive logon: Display user information when the session is locked
* **Autoriser que le group Admin (S403\Domain Admins) à ajouter un pc dans le domain** : Computer > Policies > Windows Settings > Security Settings > Local Policies > Users Rights Assignment - Add workstations to domain
* **Protéger nos DC, en appliquant une GPO sur leurs OU en renommant et activant le compte admin local** : TBoreux
* **Supprimer IPv6** : après l'ajout amd Computer > Policies > Network > IPv6 Configuration - Enabled + liste Desabled all IPv6 components
* **Prompt pour l'échéance du password** : Computer > Policies > Windows Settings > Security Settings > Local Policies > Security Options - Interactive logon: Prompt user to change passwod
* **Password policy (méthode sauvage)** : la politique étant gérée par les DC, ce sont des clés Computers qui seront répercutées sur tous les object à password du domaine. Computer > Policies > Windows Settings > Security Settings > Account Policies > Password Policy
* **Password policy (méthode moderne)** : via la console `dsac`
* **AppLocker (Pré-requis : min Win client enterprise | Application Identity service automatic) executable/scripts/...** : Computer > Policies > Windows Settings > Security Settings > Application Control Policies > AppLocker > [Types] - Create Default Rules | Add Rules pour des "exceptions". Publisher = autoriser/refuser selon l'éditeur. Hash = autoriser/refuser cet executable bien précis.
* **Removable device** : User > Policies > Adminiistrative Templates > System > Removable Storage Access - All Removable Storage Classes: Deny All Access (Disabled dans keep cool et unabled dans Default User Settings)
* **Ajouter des logiciels** : Policies > Software Settings > Software installation - New Package (.msi seulement !). On utilise un path pérénisé via un DFS. En ajoutant le .msi, dans l'onglet Modifications, il faut ajouter le fichier .mst de réponse.
* **Icônes sur le bureau** : Computer/~~User~~ > Preferences > Windows Settings > Shortcuts (C:\Utilisateurs\Public\ fusion avec le profil utilisateur).
* **Controle d'accès** : 
* **Roaming profiles** : Select user dans `dsa` > Properties > Profile > Profile path - \\domain\namespace\Roaming\%username%



* **Changer la OU par defaut d'un nouvel ordinateur du domain** : ajouter un object computer dans AD. Attention, le nom de la machine doit correspondre au nom de l'object ! OU, par `adciedit` et modififier les entrailles de l'AD. Une fois la GPO link, on sera logoff/logon !

## Registery

`regedit`

### NumLock

**Attention pour les netbooks sans pavé numérique.**

1. Editer "InitialKeyboardIndicators"="2" dans HKEY_USERS\.DEFAULT\Control Panel\Keyboard\
2. Pousser la clé modifiée pour le domaine : Default Computer Settings > Préférences > Windows Settings > Registry - New... Registry Wizard

## Scripts

### Changer le mot de passe du compte guest

```cmd
net user BrolCourt BrolCourt1234
net user BrolCourt /active:no
```

Copier GuestPwd.cmd du bureau dans le dossier des scripts de la GPO (C:\Windows\SYSVOL\sysvol\salle403.local\...), applicable dans Computer > Windows Settings > Scripts > Startup/Shutdown ou User > Policies > Windows Settings > Scripts > Logon/Logoff
