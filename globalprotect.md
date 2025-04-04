# GlobalProtect

## Basic troubleshooting

If GlobalProtect is not working, it is best to do some basic troubleshooting:

* Is it a DNS problem?
* Is the IP address reachable?
* Checking local routes.

## Log files

In the output of
On Linux, the directory `/opt/paloaltonetworks/globalprotect` has several log files:

```text
bvandewoestyne@BVANDEW-70TZQ73:/opt/paloaltonetworks/globalprotect$ ls -al *.log
-rw-r--r-- 1 root root   17645 Mär 31 12:48 install.log
-rw-r--r-- 1 root root 1685843 Apr  2 12:15 pan_gp_event.log
-rw-r--r-- 1 root root 5040139 Apr  2 12:16 PanGpHip.log
-rw-r--r-- 1 root root 9273403 Apr  2 12:16 PanGpHipMp.log
-rw-r--r-- 1 root root 6073540 Apr  2 12:19 PanGPS.log
```

## Linux networking info

In the output of

```text
ip a
```

the `gpd0` interface is created by the GlobalProtect VPN application.  As long as the VPN is not up, the status will be:

```text
bvandewoestyne@BVANDEW-70TZQ73:~$ ip address show dev gpd0
5: gpd0: <POINTOPOINT,MULTICAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 500
    link/none
```

From the moment you are connected, that status will become

```text
bvandewoestyne@BVANDEW-70TZQ73:~$ ip address show dev gpd0
5: gpd0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UNKNOWN group default qlen 500
    link/none 
    inet 10.60.30.239/32 scope global gpd0
       valid_lft forever preferred_lft forever
```

## Getting help

* [paloalto LIVEcommunity - GlobalProtect Discussions](https://live.paloaltonetworks.com/t5/globalprotect-discussions/bd-p/GlobalProtect_Discussions)

## Known issues

* [GlobalProtect Embedded Browser opens but page displayed is blank (SAML)](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA14u000000PRFuCAO)
