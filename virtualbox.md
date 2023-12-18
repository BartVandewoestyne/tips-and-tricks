# Installing guest additions

NOTE THAT THE GUEST ADDITIONS MUST BE INSTALLED ON THE VM SYSTEM, NOT THE GUEST/HOST SYSTEM!

## Ubuntu 20.04

To install the Virtualbox guest additions on Ubuntu 20.04 LTS system using the terminal, you will need to install the following packages from the Ubuntu official repository by executing the below-mentioned commands:
```
$ sudo add-apt-repository multiverse
$ sudo apt install virtualbox-guest-dkms virtualbox-guest-x11
```

# Using guest additions

## Shared Clipboard

Activate the Shared Clipboard Feature
The Virtualbox guest additions provides a bi-directional shared clipboard option that allows you to copy and paste the content between the Ubuntu virtual machine and host operating system.
To enable this feature on your system, access the menu option of your Ubuntu virtual machine. Move into the tab General / Advanced / Shared Clipboard / Bidirectional as follows:

# Other tips and tricks

To list your VMs:

```bash
VBoxManage list vms
```
