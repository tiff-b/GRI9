# Plan d'adressage IPv4

## Site de Liège

* **ID réseau global :** 10.40.3.0/26
* **Gateway :** 10.40.3.1/26
* **Première adresse IP disponible :** 10.40.3.1/26
* **Dernière adresse IP disponible :** 10.40.3.62/26
* **Plage DHCP :** 10.40.3.2/26 à 10.40.3.50/26

Par conventions, les serveurs commencent par la fin de la plage disponible. Nos clients sont clients DHCP.

* **SRV01 :** 10.40.3.62/26 (Ex Domain controller)
* **SRV02 :** 10.40.3.61/26
* **SRVO3 :** 10.40.3.60/26
* **SRV04 :** 10.40.3.59/26
* **SRV05 :** 10.40.3.58/26 (Ex Domain controller)
* **SRV06 :** 10.40.3.57/26 (Domain controller) (2k16)

## Site de Moscow

* **ID résau global :** 10.50.16.16/28
* **Gateway :** 10.50.16.17/28
* **Première adresse IP disponible :** 10.50.16.17/26
* **Dernière adresse IP disponible :** 10.50.16.30/26
* **Plage DHCP :** 10.50.16.18/28 à 10.50.16.25/28

Par conventions, les serveurs commencent par la fin de la plage disponible. Nos clients sont clients DHCP.

* **SRV07 :** 10.50.16.30/28 (Domain controller) (2k16)

## Routeurs

* **RTR01 :**
    - NiC #1 : Lan 01 - Inside - 10.40.3.1/26
    - NiC #2 : Lan O2 - Outside - 91.183.16.38/24 (GTW : 91.183.16.1)
* **RTR02 :**
    - NiC #1 : Lan 02 - Proximus - 91.183.16.1/24
    - NiC #2 : Lan 03 - mTelecom - 84.16.38.1/24
* **RTR03 :**
    - NiC #1 : Lan 03 - Outside - 84.16.38.52/24 (GTW : 84.16.38.1)
    - NiC #2 : Lan 04 - Inside - 10.50.16.17/28
