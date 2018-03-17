# Template light d'une machine virtuelle

## I. Manipulation intra Windows

### A. Mises à jour et VM tools

Il faut commencer par vérifier que windows est bien à jour. Ensuite, installer les VM tools comme d'ordinaire.

Une fois toutes les mises à jour installées, on peut supprimer les fichiers intermédiaires et temporaires qui se trouvent dans C:\Windows\Software Distribution\Download\


### B. Utilisateurs

#### 1. Activer utilisateur administrateur 

* `lusrmgr` dans la cmd pour afficher Utilisateurs et Groupes Locaux
* Dossier Utilisateurs > Clic droit sur Administrateur > Décocher "Le compte est désactivé"
* Mettre le mot de passe du compte à *zéro* via Clic droit sur Administrateur > Définir le mot de passe
* Se déconnecter et se reconnecter avec le compte administrateur
* **Pour les prochaines procédures, nous sommes donc en Administrateur !**

#### 2. Supprimer le compte créé lors de l'installation

* `lusrmgr` dans la cmd pour afficher Utilisateurs et Groupes Locaux
* Dossier Utilisateurs > Clic droit sur Compte créé > Supprimer
* `sysdm.cpl` dans la cmd pour afficher les Propriétés Systèmes
* Aller dans l'onglet Paramètres Systèmes avancés > Paramètres dans Profil des utilisateurs > Sélectionner le compte créé dans la liste > Le supprimer

### C. Programmes et fonctionnalités

* Panneau de configuration (`control`) > Programmes et fonctionnalités > Désinstaller le superflus (type Skype)
* Panneau de configuration (`control`) > Programmes et fonctionnalités > Activer ou désactiver les fonctionnalités windows (dans le panneau de gauche) > Décocher :
   * Service de localisation windows
   * Services d'impression et de numérisation de documents
   * Services XPS

### D. Désactiver Defender

Panneau de configuration (`control`) > Defender > Paramètres > Désactiver 

### E. Services Windows

`services.msc` dans la cmd et passer en manuel :

* Windows Search
* Audio Window
* Centre sécurité
* Pare-feu
* Spouleur d'impression
* Thèmes
* Planificateur de classe multimédia

*Astuce* : passer en vue standard et ordonner les services par type de démarrage.

### F. Libérer espace disque

* `cleanmgr` en cmd pour nettoyer le disque

### G. Manipulations diverses

* `sysdm.cpl` > Onglet Protection du système > Configurer > Désactiver et supprimer
* `sysdm.cpl` > Onglet Paramètres du système avancés > Paramètres des performances > Onglet Effets visuels > Choisir Ajuster afin d'obtenir la meilleure performance
* `sysdm.cpl` > Onglet Paramètres du système avancés > Paramètres des performances > Onglet Avancé > Modifier la mémoire virtuelle > Décocher Gestion automatique du fichier d'échange pour les lecteurs > Bien sélectionner le lecteur C: dans la liste > Choisir Aucun fichier d'échanger et cliquer sur Définir
* On peut supprimer le fichier pagefile.sys dans C: *Remarque* que pour voir le fichier, il faut demander à l'afficher. Dans l'explorateur > Options d'affichage > Onglet affichage > Déselectionner Masquer les fichiers protégés du système d'exploitation

## II. Manipulation dans VMware Workstation

### A. Opérations sur le disque

On peut *nettoyer* et raccourcir le disque dur .vmdk en cliquant droit sur l'onglet de la VM > Manage > Clean Up Disk. On peut automatiser cette opération après chaque extinction de la machine virtuelle via clic droit sur la VM > Settings > Onglet options > Advanced > Cocher Clean Up disk after Shutting down

### B. RAM

Si nous avons assez de RAM physique, nous pouvons demander à VMware d'utiliser cette RAM physique plutôt que d'en virtualiser dans un fichier .vmem

Dans le fichier .vmx, ajouter : mainMem.useNamedFile = "FALSE"

Si par après, on ne veut plus utiliser la RAM physique, on peut toujours commenter cette instruction en la commancant par un point-virgule.
