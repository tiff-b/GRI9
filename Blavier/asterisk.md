# Installation d'Asterisk

## I. Pré-requis

### A. Proxy

#### 1. Network Manager

Il suffit de paramétrer le serveur mandataire en GUI dans le network manager

#### 2. yum

Modifier `/etc/yum.conf` et ajouter à la fin `proxy=http://192.168.4.4:8080`

#### 3. SVN

Modifier `/home/s602/.subversion/servers` : decommenter dans [global] et ajouter nos infos
```
[global]
http-proxy-host = 192.168.4.4
http-proxy-port = 8080
http-proxy-compression = no
```

#### 4. wget

Modifier `/etc/wgetrc` : décommenter les lignes et les compléter
```
https_proxy = http://192.168.4.4:8080/
http_proxy = http://192.168.4.4:8080/
ftp_proxy = http://192.168.4.4:8080/
```

### B. Mettre à jour

Modifier `/etc/yum.repos.d/CentOS-Base.repo` (voire en faire aussi une copie, au cas où)

1. Commenter dans [update] la ligne mirrorlist
2. Changer la ligne baseurl dans [update] en `baseurl=http://belenos.corail.be/pub/linux/ftp.centos.org/7/updates/x86_64/`
3. Ajouter une ligne dans [update] : `proxy=_none_`


### C. Dépendances à installer

```
sudo yum install -y epel-release dmidecode gcc-c++ ncurses-devel libxml2-devel make wget openssl-devel newt-devel kernel-devel sqlite-devel libuuid-devel gtk2-devel jansson-devel binutils-devel svn
```

## II. Installation

1. Créer un dossier : `sudo mkdir /usr/src/asterisk/`
2. S'y déplacer : `cd /usr/src/asterisk/`

### A. DAHDI

1. Télécharger sur le site asterisk.org l'archive
2. Créer un dossier dahdi
3. Désarchiver l'archive dans le dossier dahdi
4. Depuis le dossier dahdi
    * `make`
    * `sudo make install`
    * `sudo make config`

### B. LIBRI

1. Télécharger sur le site asterisk.org l'archive
2. Créer un dossier libri
3. Désarchiver l'archive dans le dossier libri
4. Depuis le dossier libri
    * `make`
    * `sudo make install`

### C. ASTERISK

1. Télécharger sur le site asterisk.org l'archive
2. Créer un dossier asterisk
3. Désarchiver l'archive dans le dossier asterisk
4. Depuis le dossier asterisk
	  * `contrib/scripts/get_mp3_source.sh`
    * `./configure --libdir=/usr/lib64`
    * `make menuselect` et sélectionner :
        - Addon: res config mysql et format_mp3
	- Extras Sounds Packages : EN_WAV, EN_ALAW, EN_GSM, FR_WAV, FR_ALAW et FR_GSM
	- Core sounds package: EN_WAV, EN_GSM, FR_WAV et FR_GMS
	- Music on hold : Wave et GSM
	- Save et Exit
    * `make`
    * `sudo make install`
    * `sudo make samples`
    * `sudo make progdocs`
    * `sudo make config`

4. Démarrer le service : `sudo service asterisk start`

## III. Vérifier l'installation

Pour vérifier asterisk : `sudo asterisk -rvv` et dans cette console, on peut taper `core show help` pour voir l'aide. On tape `exit` pour en sortir.
