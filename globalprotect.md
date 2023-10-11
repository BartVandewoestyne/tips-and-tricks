If GlobalProtect is not working, it is best to do some basic troubleshooting:

* Is it a DNS problem?
* Is the IP address reachable?
* Checking local routes.

# Linux info

In the output of
```
ip a
```
the `gpd0` interface is created by the GlobalProtect VPN application.  As long as the VPN is not up, the status will be:
```
bvandewoestyne@BVANDEW-70TZQ73:~$ ip address show dev gpd0
5: gpd0: <POINTOPOINT,MULTICAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 500
    link/none
```
From the moment you are connected, that status will become
```
bvandewoestyne@BVANDEW-70TZQ73:~$ ip address show dev gpd0
5: gpd0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UNKNOWN group default qlen 500
    link/none 
    inet 10.60.30.239/32 scope global gpd0
       valid_lft forever preferred_lft forever
```