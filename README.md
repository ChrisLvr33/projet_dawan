***
# projet_dawan
***
![Diagram](projet_dawan.drawio.svg)
***
## Introduction
Ce dépôt est créé pour y déposer mon projet de fin de formation POEC d'Admin Sytèmes et Réseaux Cloud.  
Cette formation d'un peu moins de 3 mois a été dispensée par [![logo Markdown]( https://www.dawan.fr/build/images/dawan-logo.5b6f94e2.png)](https://www.dawan.fr/)
Le programme y était complet, peut être un peu trop, sur une période relativement courte !  
Cette formation mériterait d'avoir une durée au moins doublée...

Pour cette fin de formation, je propose de déployer une infrastructure mail dans Virtualbox avec :
- un routeur  
- un serveur proxmox mail gateway  
- un serveur dns  
- un serveur mail  
- et un serveur webmail.
Le but de ce déploiement est de l'automatiser au maximum pour pouvoir le redéployer rapidement.
***
## Etapes
### Etapes 1
Le serveur servant de routeur et celui pour proxmox non pas été automatisés.
1. Pour le routeur:  
C'est une VM avec 2 interfaces réseaux :  
- une en mode pont pour faire le lien vers la box  
- et une en réseau privé qui servira de passerelle pour le réseau privé.  
Sur cette VM est installée Ubuntu server 22.04 pour laquelle il y a très peu de configuration :  
- Modification du fichier `/etc/sysctl.conf` en y décommentant cette ligne  
```
net.ipv4.ip_forward=1
```
Ensuite, appliquer la modification avec la commande `sysctl -p`  
- Ajouter une règle de NAT dans `iptables`  
```
iptables -t nat -A POSTROUTING -o < nom_int_reseau_mode_pont > -j MASQUERADE
```
Et installer le paquet iptables-persistent pour rendre persistant cette règle  
```
apt install iptables-persistent
```
2. Pour PMG : Proxmox Mail Gateway 
