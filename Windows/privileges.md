# Droits et Permissions

## I. Notions

### A. Différence droits/permissions

* Droit = aptitude à pouvoir faire quelque chose (*Ex: ouvrir une session, changer l'heure*).
* Permission (NTFS/Partage) = type d'accès que l'on octroit à un dossier/fichier.

### B. Groupes

*Un groupe est un objet qui contient d'autres objets. Des privilèges appliqués à un groupe s'appliquent à tous les objets membres du groupes.*

#### Portée des groupes

| Type | Étendue | Membre |
|:-----|:--------|:-------|
| **Groupe local** (GL) | Limitée<br />- *Exploitable sur la machine où il a été créé* | Très souple<br />- *Objet local*<br />- *Objet provenant d'une communauté de sécurité avec laquelle il y est en confiance* |
| **Groupe local domanial** (GLD) | Limitée<br />- *Exploitable entre les DC* | Très souple<br />- *Objet local*<br />- *Objet provenant d'une communauté de sécurité avec laquelle il y est en confiance* |
| **Groupe global** (GG, +répandu) | Grande<br />- *Exploitable sur la machine où il a été créé*<br />- *Exploitable dans la communauté de sécurité* | Limité<br />- *Objet provenant de sa communauté de sécurité* |
| **Groupe universel** (GU) | Grande<br />- *Exploitable sur la machine où il a été créé*<br />- *Exploitable dans la communauté de sécurité* | Très souple<br />- *Objet local*<br />- *Objet provenant d'une communauté de sécurité avec laquelle il y est en confiance* |

- GLD = GL mais sur les DC
- Attention aux ressources systèmes demandées par les GU.
- On essaie d'utiliser le plus souvent des groupes locaux (D) pour attribuer les permissions, c'est plus rapide. Politique AGLP.

#### Types de groupes

1. Sécurité : possède un id de sécurité et permet donc de se faire octroyer des privilèges. Peut aussi servir comme groupe de distribution.
2. Distribution : permet pour la distribution d'informations (*ex : groupe de messagerie*). On peut le faire évoluer en sécurité mais pas l'inverse.

## II. Sharing

* La permission **read** sur un share équivaut à lire - exécuter - copier.
* La permission **change** implique **read** et équivaut à tous, sauf le changement des permissions.
* La permission **full control** implique **read** et **change** et peut tout faire, même changer les permissions.

Lorsqu'on est soumis à des permissions de partage et de NTFS, on est soumis aux permissions les plus restrictives.

**Best practice** : Everyone = Change en sharing et on peaufine avec les permissions NTFS.

## III. NTFS

Le NTFS est un format de fichiers qui nécessite l'attribution de permissions pour pouvoir y accéder. Une permission NTFS agit localement. Un Deny a toujours priorité sur un Allow.

Si on est dans plusieurs groupes et que les permissions de ces groupes sont différentes, on cumule les permissions de chaque groupe (les plus permissives et attention à la priorité du Deny).

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

### C. Permissions avancées

1. Applies to : où appliquer les permissions du groupe ? 
2. 

### D. Divers

#### 1. Access-Based Enumeration

*Affiche uniquement les fichiers et dossiers auxquels un utilisateur a les permissions d'accéder (permission au minimum Read)*

Sur le file system : Server Manager > File and Storage Services > Shares > Dossier - Properties > Settings > Enable access-based enumeration
