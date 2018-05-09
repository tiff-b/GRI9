# Partager un dossier linux via samba

## I. Partager un dossier

1. Installer samba : `sudo apt-get install samba`
2. Créer les dossiers à partager et vérifier les permissions
3. Modifier le fichier `/etc/samba/smb.conf` en ajoutant un [bloc] pour chaque partage. **REMARQUE, en cas de problème, il existe une copie du fichier de base dans /usr/share/samba/smb.conf**

```sh
[share_name]
    comment = Commentaire
    path = /chemin/du/dossier/partagé
    browseable = yes|no                         # (le partage est-il visible ?)
    read only = yes|no                          # OU writeable = no|yes
    valid users = utilisateur_autorisé 
              # = %s pour la variable username dans le répertoire home
    # OU guest ok = yes|no 
    create mode = 0644                          # (permission à la création d'un fichier)
    directory mode = 0755                       # (permission à la création d'un dossier)
```

4. Tester si nos blocs sont corrects avec `testparm`
5. Si un utilisateur est spécifié, il faut l'ajouter aux utilisateurs samba : `smbpasswd -a user`
6. Redémarrer les services

```shell
sudo service smbd restart
sudo service nmbd restart
```

## II. Vérifier notre partage

* `smbtree` : affiche les partages de tout le réseau
* `testparm` : vérifie que nos blocs sont corrects
* `smbcliebt -L <host> -U <user>` : teste les partages pour l'utilisateur
* `smbstatus` : affiche les infos des connections Samba actuelles
* `nmblookup [<NetBIOS>] [-A <IP>]` : donne des infos spécifiques aux machines microsoft
* `smbclient -U <user> //<host>/<share_name>` : connexion en ligne de commande (version terminal de la Connexion à un Serveur dans l'explorateur)
