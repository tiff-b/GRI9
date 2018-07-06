# Installation Drupal

## Script d'installation

mydrush.sh

```bash

#!/bin/bash

DIR=$1
DB=$2

echo "> Installation de Drupal dans $DIR"
cd /var/www/
if [ ! -d $DIR ] ; then 
	sudo drush dl drupal-7 --drupal-project-rename=$DIR
	
	echo ">>> Configuration de Drupal"
	cd /var/www/$DIR
	sudo drush si --account-name=ttbb --account-pass=abc123 --db-url=mysql://root:abc123@localhost/$DB -y
	sudo chmod -R 777 /var/www/$DIR/sites/default/files/
	
	echo ">>> Installation des langues depuis /var/www/.lang/"
	sudo drush en locale -y
	sudo drush language-add fr
	sudo drush language-default fr
	sudo drush language-import fr /var/www/.lang/drupal-7.59.fr.po

	echo ">>> Plugins"
	sudo drush en date ctools references nodereference_url email file_entity http_proxy media media_youtube pathauto simple_gmap views wysiwyg -y	
else
	echo "Le dossier $DIR existe déjà !"
fi
```

## Modules

### Modules installés

1. Coeur
	* Block
	* Color
	* Comment
	* Contextual links
	* Dashboard
	* Database logging
	* Field
	* Field SQL Storage
	* Field UI
	* File
	* Filter
	* Help
	* Image
	* List
	* Locale
	* Menu
	* Node
	* Number
	* Options
	* Overlay
	* Path
	* RDF
	* Search
	* Shortcut
	* System
	* Taxonomy
	* Text
	* Toolbar
	* Update Manager
	* User
	
2. Chaos Tool Suite
	* Chaos tools
	* Chaos tools (CTools) Plugin Example
	
3. Date
	* Date
	* Date API
	* Date Contextual
	* Date Popup
	* Date Views
	
4. Features
	* Date Migration Example

5. Fields
	* Email
	* Node References
	* Node Reference URL Widget
	* References
	* References UUID
	* User Reference
	
6. Interface Utilisateur
	* Wysiwyg (télécharger ckeditor_4.9.2_full.zip et `unzip` dans /var/www/site_web/sites/all/libraries/)

7. Média
	* File Entity
	* Media
	* Media Bulk Upload
	* Media Field
	* Media Internet Sources
	* Media WYSIWYG
	* Media WYSIWYG View Mode
	* Media: Youtube

8. Other
	* HTTP Proxy
	* Pathauto
	* Simple Google Maps
	* Token

9. Views
	* Views
	* Views UI
	
### Modules à configurer

# Backup drupal et mise à jour

1. Mettre le site hors ligne 
	* Via le site : Configuration > Mode maintenance - Mettre le site en maintenance
	* En CLI : `sudo drush vset maintenance_mode 1 # 0 pour sortir du mode maintenance.`
2. Depuis /var/www/itcorail.be `sudo drush sql-dump [--gzip] --result-file=/home/tiffanie/itcorail_backup_060718`
3. Mettre à jour drupal `sudo drush up drupal -y`
4. Remettre le site en ligne
