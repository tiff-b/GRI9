# Droits et Permissions

# I. Notions

* Droit = aptitude à pouvoir faire quelque chose (*Ex: ouvrir une session, changer l'heure*).
* Permission (NTFS/Partage) = type d'accès que l'on ocroit à un dossier/fichier.
* Groupe = objet qui contient d'autres objets.

## II. Sharing

* La permission **read** sur un share équivaut à lire - exécuter - copier.
* La permission **change** implique **read** et équivaut à tous, sauf le changement des permissions.
* La permission **full control** implique **read** et **change** et peut tout faire, même changer les permissions.

## III. NTFS

Le NTFS est un format de fichiers qui nécessite l'attribution de permissions pour pouvoir y accéder. Une permission NTFS agit localement. Un Deny a toujours priorité sur un Allow.

### B. Concepts élémentaires

* **H**éritage : une permission NTFS d'un dossier se transmet à ses enfants et les permissions héritées sont cadenassées.
* **P**ropagation implicite : une modification de permission d'un parent est propagée en direct aux enfants.
* Le groupe Système, c'est la machine en elle-même.
