# UniFi Controller Provisioner

Here,  we'll discuss how to provision a freshly imaged SD card to run UniFi Controller software.

## Creating Base Image

### STEP 1
Spin-up & SSH into the Vagrant box if you are not using Linux.
```shell
vagrant up && vagrant ssh
cd base_image
```

### STEP 2
Run the script with `sudo`.
```shell
sudo ./init-base.sh
```

## Provisioning Raspberry Pi

We use `Ansible` for this. If you don't have it on your computer, go [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) 
to get it done.

### STEP 1 
Goto `provision` directory & install prerequisites (one-off thing)
```shell
ansible-galaxy install -r requirements.yml
```

### STEP 2
Initialise Raspberry Pi 
```shell
ansible-playbook -i raspberrypi.local, -u pi initialise.yml -k
```

##### STEP 3 - INITIALISE FOR DEV
Run
```shell
ansible-playbook -i unifi-controller.local, -u pi initialise_dev.yml -k
```

### STEP 4 - Install dependencies & UniFi Controller
```shell
ansible-playbook -i unifi-controller.local, -u pi install.yml
```

### STEP 5 - INITIALISE FOR PROD
```shell
ansible-playbook -i unifi-controller.local, -u pi initialise_prod.yml
```

### TROUBLESHOOTING
#### Changed host key error
Just run, 
```shell
ansible-playbook -i unifi-controller.local, ssh_keyscan.yml
```
or
```shell
ssh-keyscan unifi-controller.local >> ~/.ssh/known_hosts 
```

#### No SSHPASS error
If you received the following error when trying to connect to the hosts with password (with `-k`)
```shell
fatal: [raspberrypi.local]: FAILED! => {"msg": "to use the 'ssh' connection type with passwords or pkcs11_provider, you must install the sshpass program"}
```
then run the following (on Mac),
```shell
brew tap esolitos/ipa
brew install sshpass
```
