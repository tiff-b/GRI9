# I. Aide

* `man [commande]` : page du manuel concernant la *commande*
* `info [commande]` : encyclopédie de la *commande*
* `[Commande] --help` : liste des options possibles de la *commande*

# II. Fichiers et dossiers

* `pwd` : affiche le chemin du dossier dans lequel on est
* `cd [/path/]` : change le dossier actuel de travail en */path/* (= se déplacer)
* `ls [/path/]` : liste les fichiers dans */path/*. Si pas spécifié, dossier actuel
     * `-a` : liste aussi les fichiers cachés (commencent par un .)
     * `-l` : affiche les métadatas des fichiers (permission, nombre de lien, user et group owner, taille, dernière modif, nom)
     * `-h` : souvent couplée avec -l, affiche la taille en human readable size
     * `-d` : souvent couplée avec -l, affiche les infos sur le dossier actuel, plutôt que des fichiers dans le dossier
     * `-R` : affichage récursif
     * `-r` : affiche à l'envers, peut-être couplé avec -S et -t
     * `-S` : affiche les plus gros fichiers en premier
     * `-t` : affiche les fichiers modifiés dernièrement en premier
* `cp [source] [destination]` : copie le fichier source vers destination
     * `-v` : mode verbeux, permet d'afficher un output de la copie
     * `-i` : demande yes/no pour chaque copie. Intéressant pour éviter l'overdrive. 
     * `-i -n` : permet d'éviter de répondre non à chaque overdrive demandé (-y pour oui)
     * `-r` : récursif, permet de copier des dossiers et leurs contenus
* `-mv [source] [destination]` : déplace le fichier source vers destination. Utilisé pour renommer
     * Les options de mv sont identiques à celles de cp, exception faite pour -r qui est déjà le comportement par défaut de mv
* `touch [fichier]` : créer un fichier
