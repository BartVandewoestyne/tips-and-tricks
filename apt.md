# apt

## Overview of commands

```bash
sudo apt update         # update list of available packages
sudo apt upgrade        # upgrade the system by installing/upgrading packages
sudo apt install <pkg>  # install packages
sudo apt remove <pkg>   # remove packages
sudo apt search <term>  # search in package descriptions
```

## Advanced commands

To print out the configured APT (or [PPA](https://help.launchpad.net/Packaging/PPA)) repositories and their priorities (also known as pinning preferences):

```bash
apt policy
```

And look at the first ones. See also [How to list and remove PPA repository on Ubuntu 20.04 Linux](https://linuxconfig.org/how-to-list-and-remove-ppa-repository-on-ubuntu-20-04-linux)

## References

* `apt --help`
* [Ubuntu Server documentation - Install and manage packages](https://documentation.ubuntu.com/server/how-to/software/package-management/index.html)
