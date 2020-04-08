Role Name
=========

Ce role ansible permet de créer une infra (vnet, subnet, IP, ..., VM)  dans Azure.

**Fonctionnement :**
Le playbook infra.yml exécute le rôle. 
Il crée tout l'environnement Azure pour déployer la ressource (ici une VM) :
- un groupe de ressource qui va contenir toutes les ressources
- un réseau virtuel (vnet) dans lequel se trouve un sous réseau (subnet)
- une IP publique statique pour la VM
- une carte réseau avec un nom explicite pour la VM
- un groupe de sécurité d'application auquel la VM est rattachée qui n'autorise que certains ports (SSH)
- une machine virtuelle Linux (Centos).

Mais il est possible de créer avec ce role plus qu'une machine virtuelle. Il faut dans ce cas améliorer les playbooks.


Requirements
------------
Pour utiliser ce rôle, il faut d'abord créer dans le shell d'Azure le principal service et configurer les credentials :
**Créer un principal de service**
```
user@Azure:~$ az ad sp create-for-rbac --name ServicePrincipalName
```
**Créer un fichier d’informations d’identification Ansible**
1. Créer le fichier d'identification
```
mkdir ~/.azure
vi ~/.azure/credentials
```
2. Coller les lignes suivantes (à adapter)
```
[default]
subscription_id=<your-subscription_id>
client_id=<security-principal-appid>
secret=<security-principal-password>
tenant=<security-principal-tenant>
```

Pour plus de détails, voir le lien [Comment créer un principal service et vérifier l'installation de ansible](https://docs.microsoft.com/fr-fr/azure/ansible/ansible-install-configure#create-azure-credentials)


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost
      remote_user: root
      roles:
         - { role: infra }

License
-------

BSD

Author Information
------------------
TassyK
