# I. Roles et Features installés sur Domain Controler

## A. Active Directory Domain Service

*Permet le stockage des informations à propos des objets du domaine. Créer un rôle de **domain controller**.*

1. Add Roles and Features
2. Role-based or feature-based installation
3. Selectionner le Serveur
4. Active Directory Domain Services
5. Pas de features

Une fois le rôle ajouté, on a la possibilité de promouvoir notre serveur en Domain Controller.

1. Choisir Add a New Forest, puisqu'on commence un nouveau domaine.
2. Root domain name : doit être au minimum de niveau 2 (*salle403.local*)
3. Options par défaut
4. Netbios name, pour rétrocompatibilité (*S403*)
5. On laisse les chemins par défaut
6. On installe

## B. DNS

*Permet de faire la résolution de nom entre un nom et une IP et vice-versa. Souvent installé sur le DC.*

1. En installant le DC, on a installé en même temps le serveur DNS.
2. Vérifier que dans `ncpa.cpl`, le DNS est renseigné avec une IP autre que localhost
3. Le DNS créé automatiquement sa Forward Lookup Table, nous devons créer une Reverse Lookup Table
     * `dnsmgmt` > Server_name > Reverse Lookup Zones > New Zone
     * Primary Zone > Check the box > DEFAULT > IPv4 > Network ID > NEXT > FINISH
4. Créer le pointeur de notre serveur :
     * Reverse > New PTR > Host IP - FQDN Default - Host : name_server.name_forest
5. Vérification via `nslookup`

## C. WINS

*C'est l'ancêtre DNS de Windows, utilise les noms NetBIOS.*

**Remarque : il faudra spécifier l'IP du WINS serveur dans les configurations réseaux des clients/members, maintenant.**

1. Add Roles and Features
2. Role-based or feature-based installation
3. Selectionner le Serveur
4. Pas de Rôle
5. WINS Server comme Features

## D. DHCP Server

*Permet au serveur d'envoyer des IPs et autres configurations réseaux automatiquement aux clients DHCP.* 

1. Add Roles and Features
2. Role-based or feature-based installation
3. Selectionner le Serveur
4. DHCP Server
5. Pas de features

Une fois installé, on peut le configurer via la console de management `dhcpmgmt`

1. Clic droit sur le serveur > Authorize
2. Dans IPv4, New Scope
     * Name (*Lan01-Windows*)
     * Pool start & end (*10.40.3.2 - 10.40.3.50*)
     * lenght = mask (*255.255.255.192*)
     * Pas d'exclusion
     * Lease = 1jour
     * Oui, je veux configurer les options que le DCP envoit maintenant
          * Routeur : pour le moment, on n'en a pas
          * Parent domain : default (*salle403.local*)
          * WINS Server : je mets l'IP et ADD (*10.40.3.62*)
     * Oui, je veux activer le scope
     
## E. DFS

*Structure logiquement les dossiers partagés éparpillés sur des Members. Pérénité des chemins d'accès.*

1. Add Roles and Features
2. Role-based or feature-based installation
3. Sélectionner le Serveur
4. File and Storage Services > File and iSCSI Services > DFS Namespaces
5. Pas de Features

Pour le configuer, on utilise sa console de management : `dfsmgmt`, partie Namespaces

# II. Roles et Features installés sur des Members

On peut gérer les roles et features des Members via le Domain Controler.

Server Manager > Create a Server Group > Nom du groupe > Active Directories - Find... > Mettre à droite tous les serveurs qu'on veut

## A. FRS (File Replication Service)

*Permet aux Members de répliquer les fichiers entre eux.*

1. Add Roles and Features
2. Role-based or feature-based installation
3. Sélectionner le Serveur
4. File and Storage > File and iSCSI > DFS Replication > NEXT

On le configure via la console de management `dfsmgmt`

Dans la partie Namespaces, on ajoute un Folder Target à un de nos folders. Il faut que la target soit déjà créée et donc qu'un dossier partagé ait déjà été créé.

!! Pour avoir deux Folder Target, il faut qu'ils soient sur deux Members différents !!

Une fois la target ajoutée, on nous demande si on veut synchroniser. OUI, donc on a un wizard pour créer une politique de réplication. Pour le moment, NEXT, FULL MESH et REPLICATE FULL BANDSWISH.

**!! Primary Member = partage qui va être copié sur notre nouvelle target. Si on inverse, on erase toutes nos data !!**

## B. Remote Server Administration Tools

*Depuis un client, permet de gérer les serveurs à distance.*

1. Télécharger le .msu qui correspond à la version et la langue du client (FR 32bits)
2. L'installer sur le client. On a maintenant accès aux consoles de management
