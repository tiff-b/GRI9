# Droits et Permissions

## I. Notions

### A. Différence droits/permissions

* Droit = aptitude à pouvoir faire quelque chose (*Ex: ouvrir une session, changer l'heure*).
* Permission (NTFS/Partage) = type d'accès que l'on ocroit à un dossier/fichier.

### B. Groupe

*Un groupe est un objet qui contient d'autres objets.*

## II. Sharing

* La permission **read** sur un share équivaut à lire - exécuter - copier.
* La permission **change** implique **read** et équivaut à tous, sauf le changement des permissions.
* La permission **full control** implique **read** et **change** et peut tout faire, même changer les permissions.

## III. NTFS

Le NTFS est un format de fichiers qui nécessite l'attribution de permissions pour pouvoir y accéder. Une permission NTFS agit localement. Un Deny a toujours priorité sur un Allow.

Si on est dans plusieurs groupes et que les permissions de ces groupes sont différentes, on cumule les permissions de chaque groupe (ADD et attention à la priorité du Deny).

### A. Concepts élémentaires

* **Héritage** : une permission NTFS d'un dossier se transmet à ses enfants et les permissions héritées sont cadenassées.
* **Propagation implicite** : une modification de permission d'un parent est propagée en direct aux enfants.
* Le groupe Système, c'est la machine en elle-même.

### B. Permissions de bases

De la plus restrictive à la plus laxiste :

1. L  - List Folder Content (folder) : se balader, voir ce qu'il se trouve dans un dossier.
2. R  - Read : lire un fichier (mais pas un exécutable !).
3. RX - Read & Execute : lire et exécuter.
4. W - Write : modifier le contenu et ajouter du contenu, pas contenant (absurde sans R).
5. M - Modify : modifier le contenu et contenant.
6. Full Control : toutes celles d'avant, plus P (changer les permissions) et O (propriétaire).
7. Special Permission : permissions personnalisées
