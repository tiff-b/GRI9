# Virtual Hosts Apache 2

*Avec une même instance du serveur apache2, on peut supporter plusieurs sites différents.*

## Sur le serveur

1. Éditer le fichiers `/etc/hosts` (ou DNS plus tard) pour ajouter la correspondance 127.0.1.1 www.domain.ext
2. Créer les dossiers des sites dans `/var/www/` sous la forme domain.ext
3. Dans `/etc/apache2/apache2.conf` vérifier qu'un bloc Directory nous permet l'accès
4. Dans `/etc/apache2/sites-available/`, on copie le fichier 000-default.conf plusieurs fois en domain.ext.conf
5. On modifie ces nouveaux fichiers :
     * DocumentRoot /var/www/domain.ext
     * ServerName www.domain.ext
6. Activer les sites fictifs avec `a2ensite ddomain.ext.conf` et puis reload le service `sudo service apache2 reload`

## Sur les clients

1. Éditer le fichiers `/etc/hosts` (ou DNS plus tard) pour ajouter la correspondance ip.du.serveur www.domain.ext

# Apache Sécurisé

*Utilisé un certificat pour nos virtuals hosts*

1. Installer le module : `sudo a2enmod ssl`
2. Demande de certificat : `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout itcorail.key -out itcorail.crt`
3. Créer /etc/apache2/ssl et y déplacer itcorail.key et itcorail.crt
4. Adapter notre virtual host. Dans /etc/apache2/sites-available
    - Copier default-ssl.conf en itcorail
        * Server Name www.itcorail.be
        * DocumentRoot /var/www/itcorail.be
        * SSLCertificateFile /etc/apache2/ssl/itcorail.crt
        * SSLCertificateKeyFile /etc/apache2/ssl/itcorail.key
    - Désactiver l'ancien virtual host `sudo a2dissite itcorail.be.conf` et activer le nouveau `sudo a2ensite itcorail.be-ssl.conf`
    - `sudo service apache2 reload`
