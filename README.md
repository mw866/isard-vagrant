# IsardVDI on Virtualbox

[IsardVDI](https://github.com/isard-vdi/isard)  writes to the the host environment.
Having issue with that? Try running it in a VM.

## Prerequite
1. Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
1. Install [Vagrant](https://www.vagrantup.com/docs/installation)


## Quickstart
On the host machine, run
```
vagrant up
vagrant ssh
```

On the guest VM, run
```
cd /vagrant_data/
docker-compose pull
docker-compose up -d
```
The open https://localhost using browsers on on the host machine

## Known Issues and Troubleshooting

### Isard On MacOs
Issue with timezone. 
https://github.com/isard-vdi/isard/issues/174
## Isard on Google Cloud VM
On the Cotainer Optimized, docker does not have access to the host machine.
You can get around this with other machine types, but it's unclear if nested virtualization is holsted. 

### Isard Wizard" "Can't contact any hypervisor with virtualization available."
Vagrant shall take care of it already. If not, enabled it manually with the commands below.
```
vboxmanage list vms
vboxmanage modifyvm $VM_NAME --nested-hw-virt on
```
https://docs.oracle.com/en/virtualization/virtualbox/6.0/admin/nested-virt.html
https://stackoverflow.com/questions/54251855/virtualbox-enable-nested-vtx-amd-v-greyed-out

### VM Disk space too small or large (default: 50GB)

Option 1: resize the drive with `VBoxManage`
https://tuhrig.de/resizing-vagrant-box-disk-space/

Option 2: use `vagrant-disksize` plugin https://github.com/sprotheroe/vagrant-disksize

### Chrome block self-signed certs at https://localhost
https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate

## Reference

* https://github.com/isard-vdi/isard

* https://docs.docker.com/compose/install/

* https://technology.amis.nl/2018/05/21/rapidly-spinning-up-a-vm-with-ubuntu-and-docker-on-my-windows-machine-using-vagrant-and-virtualbox/

