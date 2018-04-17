# Création d'un disque iSCSI sur un serveur FreeNAS11.1 ou Nas4Free11.4

## Pré-requis

| Hardware | **FreeNAS** | **Nas4Free** |
|:--------:|:-----------:|:------------:|
| Guest OS | FreeBSD 11 64-bit | FreeBSD 11 64-bit | 
| Version | 11.1-U4 | 11-4 |
| Memory | 8GB | 8GB |
| Processors | 2 | 2 |
| Network | VMnet1 | VMnet1 |
| Hard Disk (System) | 20GB SCSI | 20GB SCSI | 
| Hard Disk (iSCSI) | 40GB SATA | 40GB SATA |
| ISO | FreeNAS-11.1-U3.iso | NAS4Free-x64-LiveCD-11.0.0.4.3252.iso |

## Installation et configuration

### Installation

| **FreeNAS** | **Nas4Free** |
|:------------|:-------------|
|Install/Upgrade <br/> [space] pour sélectionner da0 <br/> Password 987654 <br/> Boot via BIOS <br/> Shutdown <br/> Retirer l'iso|9) Install/Upgrade <br /> 1) Install (Preferred) <br /> 1) Install (preferred) <br /> cd0 <br /> da0 <br /> 8192 <br /> Enter <br /> Shutdown <br /> Enlever iso| 

### Configuration CLI

| **FreeNAS** | **Nas4Free** |
|:------------|:-------------|
| Configure Network Interfaces <br /> Interface 1 <br /> No reset <br /> No DHCP <br /> Yes IPv4 <br /> em0 <br /> 192.168.162.11/24 <br /> No IPv6 | Configure Network IP Address <br /> No DHCP <br /> 192.168.162.4/24 <br /> 192.168.162.254 GTW  <br /> DNS : 192.168.231.8 <br /> No IPv6 | 

### Configuration GUI

User : root
Password : 987654
URL : http://192.168.162.11/

Exit Wizard

System > General :
* Language : French
* Keyboard Map : Belgian ISO-8859-1 (accent keys)
* Timezone : Europe/Brussels 

Network > Config générale
* Hostname : freenas-11
* Domain : nuage.gris
* Gateway : 192.168.162.254
* DNS : 192.168.231.8 - 192.168.231.10 - 192.168.4.254
* Proxy : 192.168.4.4:8080

Mise à jour :

System > Mise à jour > Check Now (FreeNAS-11-STABLE)


