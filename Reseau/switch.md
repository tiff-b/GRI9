# Switch Layer 2 et Switch Layer 3

## I. Configuration de base

```bash
Switch> enable                  ᐅ Switch# 
Switch# configure terminal      ᐅ Switch(config)# 
Switch(config)# line console 0  ᐅ Switch(config-line)#
Switch(config)# line vty 015    ᐅ Switch(config-line)#
```

1. Hostname : `(config)# hostname <name>`
2. Protection :
    - Mode privilégié : `(config)# enable secret <password>`
    - Port console : `(config-line)# password <password>` + `(config-line)# login`
    - Port VTY : `(config-line)# password <password>` + `(config-line)# login` + `(config-line)# transport input ssh`
    - Password encryption : `(config)# service password-encryption`
    - Base locale pour les login VTY et console : `(config-line)# no password` + `(config-line)# login local`
3. Management :
    - Entrer dans la VLAN : `(config)# interface vlan 1`
    - Lui ajouter une adresse IP : `(config)# ip address <ip> <masque 255>`
    - Activer : `(config)# no shutdown`
4. Bannières :
    - MOTD : `(config)# banner motd #<msg>#`
    - Login : `(config)# banner login #<msg>#`
5. Configuration SSH :
    - Nom de domaine : `(config)# ip domain-name <domain.ext>`
    - User : `(config)# username <user> secret <password>`
    - Clé : `(config)# crypto key generate ?` pour savoir quoi utiliser + `(config)# crypto key generate <modulus|general-keys>`
    - Version 2 : `(config)# ip ssh version 2` + `(config)# show ip ssh` pour vérifier la version
6. Message d'infos ne coupent pas le prompt dans port console : `(config-line)# logging synchronous`
7. Sauvegarder la configuration : `(config)# copy running-config startup-config`
