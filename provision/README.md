# Ansible guide

Trying to give an in-depth guide to how the Ansible has set up & the order of execution AKA The Ansible Anatomy.

## Playbooks & Roles

we have 5 different playbooks executing various roles in different stages. 

In the order they should be executed & their roles, 
1. initialise
   1. basic-config
   2. change-passwords
   3. localisation
   4. set-hostname
2. initialise_dev 
   1. add-ssh-key
   2. enable-wifi
3. install
   1. upgrade
   2. install-jre
   3. install-rng-tools
   4. install-mongodb
   5. install-unifi-controller
4. initialise_prod (for `prod` only)
   1. disable-wifi
   2. remove-ssh-key
