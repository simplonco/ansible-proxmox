# ansible-proxmox

> Ces rôles Ansible n'installent pas de serveur Proxmox, ils servent simplement à configurer un Proxmox fraichement installé

## Prérequis

* Serveur Proxmox VE 6 - OVH - mais devrait fonctionner de la même manière chez d'autres fournisseurs
* Disposer d'un accès SSH

## Utilisation

1. `git clone git@github.com:simplonco/ansible-proxmox.git`
2. `cp inventory.dist inventory` et l'adapter avec vos serveurs
3.  
4. `ansible-playbook main.yml`

## Rôles

### base

* Mise à jour du système et installation de paquets aditionnels

### network

* Configuration d'interfaces supplémentaires (vmbrx)
* Installation et configuration d'un serveur DHCP local
