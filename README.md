# ansible-proxmox

> Ces rôles Ansible n'installent pas de serveur Proxmox, ils servent simplement à configurer un Proxmox fraichement installé

## Prérequis

* Serveur Proxmox VE 6 - OVH - mais devrait fonctionner de la même manière chez d'autres fournisseurs
* Disposer d'un accès SSH

## Utilisation

1. `git clone git@github.com:simplonco/ansible-proxmox.git`
2. `cp inventory.dist inventory` et l'adapter avec vos serveurs (https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
3. `cp main.yml.dist main.yml` et l'adapter à vos besoin, ajouter des interfaces supplémentaires et des réseaux pour le DHCP
4. `ansible-playbook main.yml`

## Rôles

### base

* Mise à jour du système et installation de paquets aditionnels
* Timezone Europe/Paris

### network

* Configuration d'interfaces supplémentaires (vmbr)
* Installation et configuration d'un serveur DHCP local

## Tags

Si besoin de jouer seulement certaines tâches vous pouvez commenter / décommenter les rôles dans le fichier `main.yml` ou bien utiliser les tags

| Tag | Description |
| --- | ----------- |
| `base` | Toutes les tâches du rôle base |
| `network` | Toutes les tâches du rôle network |
| `interfaces` | Configuration des interfaces |
| `dhcp` | Installation et configuration du DHCP |

## Problèmes rencontrés

* Si les interfaces supplémentaires ne sont pas dans le fichier `/etc/network/interfaces` elles ne seront pas disponibles via l'interface Proxmox
* Depuis peu (~ avril / mai 2021) le script `/etc/network/if-pre-up.d/wait_for_link_up` pose problème et on ne peut monter les interfaces, on lui demande gentillement de ne pas agir sur les interfaces vmbr1 à 9 (https://github.com/simplonco/ansible-proxmox/blob/main/roles/network/tasks/interfaces.yml#L2-L10) 
