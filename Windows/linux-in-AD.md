# Intégrer un client linux dans un active directory

[Ubuntu Help](https://help.ubuntu.com/lts/serverguide/sssd-ad.html)

1. Ajouter `<adresse ip>	ubu1804-xx.stag.corail.be ubu1804-xx` dans /etc/hosts
2. Vérifier que l'adresse IP DNS soit celle du DC dans nos paramètres réseaux
3. `sudo apt install krb5-user samba sssd chrony`
4. Vérifier que le royaume soit correct dans le bloc [libdefaults] du fichier /etc/krb5.conf `default_realm = STAG.CORAIL.BE`
5. Configurer le bloc [global] du fichier /etc/samba/smb.conf (on peut tester nos paramètres avec `testparm`

```bash
[global]

workgroup = STAG
client signing = yes
client use spnego = yes
kerberos method = secrets and keytab
realm = STAG.CORAIL.BE
security = ads
```

6. Créer le fichier /etc/sssd/sssd.conf, le `sudo chown root:root /etc/sssd/sssd.conf` et `sudo chmod 600 /etc/sssd/sssd.conf`

```bash
[sssd]
services = nss, pam
config_file_version = 2
domains = STAG.CORAIL.BE

[domain/STAG.CORAIL.BE]
id_provider = ad
access_provider = ad

# Use this if users are being logged in at /.
# This example specifies /home/DOMAIN-FQDN/user as $HOME.  Use with pam_mkhomedir.so
override_homedir = /home/%d/%u

# Uncomment if the client machine hostname doesn't match the computer object on the DC.
# ad_hostname = mymachine.myubuntu.example.com

# Uncomment if DNS SRV resolution is not working
# ad_server = dc.mydomain.example.com

# Uncomment if the AD domain is named differently than the Samba domain
ad_domain = STAG.CORAIL.BE

# Enumeration is discouraged for performance reasons.
# enumerate = true
```

7. (Re)Démarrer les services

```bash
sudo systemctl restart chrony.service
sudo systemctl restart smbd.service nmbd.service 
sudo systemctl start sssd.service					
			# Remarque, il se peut qu'on obtienne une erreur
			# lors du démarrage, c'est pas grave, on continue sans

```

8. Obtenir un ticket kerberos `sudo kinit Administrator` et le vérifier `sudo klist`
9. Joindre le domaine `sudo net ads join -k`
10. Faire en sorte qu'au logon avec un user du domain, son dossier soit créer : dans le fichier /etc/pam.d/common-session, **ajouter juste après la ligne session required pam_unix.so** `session    required    pam_mkhomedir.so skel=/etc/skel/ umask=0022`
11. On peut maintenant se connecter avec un user du domain via `su - <user_domain>`
