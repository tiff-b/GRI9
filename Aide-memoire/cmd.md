# Aide-mémoire de certaines commandes 

En ouvrant une commande windows en mode administrateur, nous sommes directement dans le dossier `C:\Windows\System32`

## Commandes générales

* `cls` : *Nettoyer* la console, nouvel écran vierge
* `dir \chemin\vers\dossier\` : se déplace dans ce dossier
* `delete fichier` : supprime le fichier
* `rd /s dossier` : supprimer le dossier
* `shutdown -l` : se déconnecter (log off)
* `resmon` : moniteur de ressource (gestionnaire de tâches plus complet)
* `wf` : firewall

## Panneau de configuration (*control panel*)

Pour accéder au control panel, on tape `control`

### Accès direct à certaines catégories du control panel

On tape : `nom.cpl`

Pour accéder à la liste des control panel accessibles, on peut les lister via `dir *.cpl` dans System32

#### Liste arbitraire

* `ncpa.cpl` : Carte réseau
* `sysdm.cpl` : Propriétés Systèmes

## Outils de configuration

Certaines *boites de dialogue* de configuration peuvent être appelées directement via la console.
On peut lister ces outils via `dir *.msc` dans System32

### Liste arbitraire

* `lusrmgr` : utilisateurs et groupes locaux
* `services.msc` : liste des services

## Programmes consoles

* `cleanmgr` : nettoyage de disque
