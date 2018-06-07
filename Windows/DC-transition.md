# DC redondance / migration

## I. Création de l'autre DC

1. On créé un SRV
2. On lui ajoute le rôle AD
3. On le promeut comme DC. Attention, on l'ajoute à une forêt existante.
4. On vérifie le DNS

## II. Synchro des rôles du DC à l'autre DC

### A. DNS

1. `dnsmgmt` > DNS - Connect to DNS > SRV05 > Vérifier que dans les propriétés de toutes les tables du DNS de SRV01 et SRV05 - Name Servers, il y a les 2 IPs.
2. Vérifier aussi Zone Transfers - Check case et only to servers listed ...
3. Dans les clients/members statiques, on indique notre autre serveur DNS. (Manuel ou avec un script/GPO)
4. `dhcpmgmt` > Dans DHCP > SRV01 > IPv4 > Scope > Scope Options > Add un server DNS dans l'option 006. Le renouvellement se fera à bail demi temps.


Best practice : dans `ncpa.cpl` du server, on indique l'autre DNS en DNS primaire, plutôt que lui-même. Qui devient donc le DNS secondaire. Au cas où l'autre server boot d'abord.

Pour la migration, on supprime toutes les références au DNS qui va mourir. Ensuite, dans `dnsmgmt`, on revérifie toutes les tables et on enlève dans Name Servers l'ancien DC?

5. Server Manager > Manage > Remove Role > Remove DNS

### B. DHCP

1. Installer le service DHCP sur notre nouveau DC et l'authorize. Tout comme l'autre fois, sauf qu'on n'active pas le scope maintenant.
2. **Méthode 1** : Dans un DC, exclure la moitié du paquet d'IP du scope et rapidement, exclure l'autre moitié sur l'autre DC.
3. **Méthode 2** : Retour case départ avec un seul scope sur SRV01. Copier la database de SRV01 et la coller dans SRV05.

```cmd
## SRV01
                              # Dans une deuxième explorateur : \\SRV05\admin$\System32\dhcp
                              
sc \\SRV05 stop dhcpserver    # Arrête le service DHCP sur SRV05
                              # puis on delete C:\Windows\System32\dhcp\*

net stop dhcpserver           # Arrête le service DHCP sur SRV01
                              # VITE puis copie C:\Windows\System32\dhcp\dhcp.mdb dans la fenêtre de SRV05

sc \\SRV05 start dhcpserver   # Redémarre le service DHCP sur SRV05
```

### C. DFS

1. Installer DFS Namespace sur SRV05
2. `dfsmgmt` > Namespace - Add Namespace to Display > salle403.local - Add Namespace Server > SRV05.salle403.local
3. On peut laisser plusieurs namespace servers et en migration, on disable ceux qui partent. Si tout se passe bien, on le supprime. Et puis on désinstalle le rôle.

### D. WINS

1. Installer la feature
2. `winsmgmt` > WINS - Add Server - SRV01. Dans chaque Replication Partners, on ajoute l'autre serveur.
3. Client statique : on change l'adresse statique
4. On change l'option dans `dhcpmgmt`
5. On supprime nos Replication Partners
6. On supprime la feature
