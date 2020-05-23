# Vagrant Skeleton - Ubuntu / Ansible / Docker

Skeleton for Vagrant deployment with ansible of Ubuntu 16.04 VM with docker

This deployment can be used in a windows environment.
For the ansible deployment the _ansible_local_provider_ is used,
no local ansible installation is needed.

## Requirements
- [Vagrant](https://www.vagrantup.com/)
- [Virtualbox](https://www.virtualbox.org/) / HyperV / [vagrant supported technology](https://www.vagrantup.com/docs/providers/)

## Usage
```bash
git clone https://github.com/iwitzky/vagrant-ansible-skeleton.git
cd vagrant-ansible-skeleton
vagrant up
```

## License
MIT / BSD

## Author Information
This Vagrant deployment was created in 2020 by [Ingo Witzky](https://github.com/iWitzky).
