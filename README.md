# README

## Preamble

This playbook assumes the following configurations:

1) The rpis has been initialized with ubuntu.
2) An external hdd is being used to store blockchain data. It will require some extra
bit of configuration to change this setup. All bitcoind/lightningd data is stored on the
external hdd and not the SD card. This is very, very intentional.
3) Two users will be running on the rpi: pi and bitcoin
4) systemd is used to manage bitcoind/lightningd processes
5) ssh keys are used instead of password authentication.

### Default layout 

```
/srv/payrank/
  ├── bitcoind
  │   ├── blocks
  │   └── bitcoin.conf
  └── lnd
      ├── data
      ├── etc/lnd.conf
      └── logs
```


## Running

```
cd ansible
ansible-playbook main.yaml -i inventory/
```

## Required Configurations

This repo does not contain an inventory directory or inventory files, as they are bespoke
to each user. However, the following sample inventory file outlines all the required
host vars for all the roles.

### Inventory

set in `rpi-lightning-node-ansible/ansible/inventory/lightning.yaml`:

```
all:
  hosts:
    example-lightning-node:
      ansible_host: 192.168.0.10
      ansible_user: ubuntu # if debian based use "pi"
```

### Host Vars

edit in `/rpi-lightning-node-ansible/ansible/inventory/host_vars/payrank-test-node.yaml`

### SSH Keys

Put your ssh keys in `rpi-lightning-node-ansible/ansible/roles/payrank/harden-ssh/files/keys`
