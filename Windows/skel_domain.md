# Créer un domaine

## I. Domain Controler

### A. Prérequis

1. `Sysprep` (après clone)
2. Hostname (sans - ou _)
3. Connexion + Static IPv4 + DNS
4. Disable IPv6
5. Automatic Pagefile
6. Firewall always off
7. Complex Password

### B. Installer Active Directory Domain Service

1. Add role active directory domain service
2. Promouvoir la machine en domain controler
     * Add new forest (name = second level min)
     * Default NEXT

### C. DNS

1. Après reboot, vérifier que DNS ne soit pas comme localhost (127.0.0.0) mais bien ip du DC
2. Create Reverse Lookup Table
     * `dnsmgmt` > Server_name > Reverse > New Zone
     * Primary Zone > Check the box > DEFAULT > IPv4 > Network ID > NEXT > FINISH
3. Reverse > Create PTR > Host IP - FQDN Default - Host : name_server.name_forest
4. Vérification via `nslookup`

### D. DHCP Server

1. Add role
2. `dhcpmgmt` > Clic droit - Authorize
3. New Scope > 
     * Name = Lan_Segment_Name
     * Pool start & end
     * lenght = mask
     * NEXT > FINISH (avec yes, qqpart, pour les options de config)

## II. Server Member

### A. Prerequis

1. `Sysprep` (après clone)
2. Connexion + Static IPv4 + DNS
3. Disable IPv6
4. Automatic Pagefile
5. Firewall always off
6. Hostname + Domain
7. `lusrmgr` > Rename Administrator en Admin

### B. Role/Feature à installer

## III. Clients

1. NewSID
2. Connexion + dynamic IPv4
3. Hostname + Domain
