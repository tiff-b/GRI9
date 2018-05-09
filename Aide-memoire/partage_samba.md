# Partager un dossier linux via samba


1. Installer samba : `sudo apt-get install samba`
2. Créer les dossiers à partager et vérifier les permissions
3. Modifier le fichier `/etc/samba/smb.conf` en ajoutant un [bloc] pour chaque partage

```sh
[share name]
    comment = Commentaire
    path = /chemin/du/dossier/partagé
    browseable = yes|no # (le partage est-il visible ?)
    read only = yes|no # OU writeable = no|yes
    valid user = utilisateur_autorisé 
              # OU %s pour la variable username dans le répertoire home
    # OU guest ok = yes|no 
    create mode = 0644 # (permission à la création d'un fichier)
    directory mode = 0755 # (permission à la création d'un dossier)
```

4. Si un utilisateur est spécifié, il faut l'ajouter aux utilisateurs samba : `smbpasswd -a user`
5. Redémarrer les services

```shell
sudo service smbd restart
sudo service nmbd restart
```
