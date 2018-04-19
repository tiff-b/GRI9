# I. Roles et Features installés sur Domain Controler

## A. Active Directory Domain Service

1. Add role active directory domain service
2. Promouvoir la machine en domain controler
     * Add new forest (name = second level min)
     * Default NEXT

## B. DNS

1. Après reboot, vérifier que DNS ne soit pas comme localhost (127.0.0.0) mais bien ip du DC
2. Create Reverse Lookup Table
     * `dnsmgmt` > Server_name > Reverse > New Zone
     * Primary Zone > Check the box > DEFAULT > IPv4 > Network ID > NEXT > FINISH
3. Reverse > Create PTR > Host IP - FQDN Default - Host : name_server.name_forest
4. Vérification via `nslookup`

## C. WINS



## D. DHCP Server

1. Add role
2. `dhcpmgmt` > Clic droit - Authorize
3. New Scope > 
     * Name = Lan_Segment_Name
     * Pool start & end
     * lenght = mask
     * NEXT > FINISH (avec yes, qqpart, pour les options de config)
     
## E. DFS

# II. Roles et Features installés sur des Members

On peut gérer les roles et features des Members via le Domain Controler.

Server Manager > Create a Server Group > Nom du groupe > Active Directories - Find... > Mettre à droite tous les serveurs qu'on veut

## A. FRS (File Replication Service)

Permet aux Members de répliquer les fichiers entre eux.

### Installation

1. Add Roles and Features
2. Role-based or feature-based installation
3. Sélectionner le Serveur
4. File and Storage > File and iSCSI > DFS Replication > NEXT

### Configuration

Console de management = `dfsmgmt`

Dans la partie Namespaces, on ajoute un Folder Target à un de nos folders. Il faut que la target soit déjà créée et donc qu'un dossier partagé ait déjà été créé.

!! Pour avoir deux Folder Target, il faut qu'ils soient sur deux Members différents !!

Une fois la target ajoutée, on nous demande si on veut synchroniser. OUI, donc on a un wizard pour créer une politique de réplication. Pour le moment, NEXT, FULL MESH et REPLICATE FULL BANDSWISH.

**!! Primary Member = partage qui va être copié sur notre nouvelle target. Si on inverse, on erase toutes nos data !!**
