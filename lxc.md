To get list on local machine

```
lxc image list
```

To list the machines you are currently running:

```
lxc list
```

or to get some more info

```
lxc list -c n,s,4,image.description:image
```

To get remote list:

```
lxc remote list
```

To create your own machine:

```
lxc launch ubuntu:18.04 ubuntu1
```

where `ubuntu` is the name of the image repository, 18.04 is the version and `ubuntu1` is the container name.

To search what images are out there:

```
lxc image alias list ubuntu:
```

or

```
lxc image alias list ubuntu: 18.04
```

To get some info on a container:

```
lxc info ubuntu1
```

To run a command on one of your containers:

```
lxc exec ubuntu1 hostname
```

To go into these containers

```
lxc exec ubuntu1 bash
```

To stop one of your containers:

```
lxc stop ubuntu1
```

To start it:

```
lxc start ubuntu1
```

To delete a container

```
lxc delete ubuntu1
```

Say you created a machine, and you setup a bunch of settings and you want to clone it:

```
lxc copy ubuntu1 ubuntu2
```

To copy over files from your machine to the lxc container:

```
lxc file push /local/file ubuntu1/remote/file
```
  
To pull a file from the container to your machine:

```
lxc file pull ubuntu1:/remote/file /local/file
```

To edit a file:

```
lxc file edit ubuntu1:/remote/file
```

To take a snapshot:

```
lxc snapshot ubuntu1
```

To restore a snapshot:

```
lxc restore ubuntu1 snap0
```

To delete a snapshot:

```
lxc delete ubuntu1/snap0
```

To make your containers available on your lan, you need to use a Bridged adapter:

```
cat /etc/netplan/50-cloud-init.yaml
```

See https://youtu.be/cqOtksmsxfg