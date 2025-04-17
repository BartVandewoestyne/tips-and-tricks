# nmap

## TCP port scanning

To scan all TCP-ports on the system with IP 10.70.70.83, trying to find which ports are open and for all open ports, try to find what service and version is running:

```sh
nmap -sSV -p- -oA tcpScan 10.70.70.83
```

* `-sS`: use a TCP SYN scan, also known as "half-open" scan.  It's fast and stealthier than a full connection scan (`-sT`)
* `-sV`: probe open ports to determine service/version info
* `-p-`: scan all 65535 ports (from 1 to 65535)
* `-oA tcpScan`: output the results to all three major formats (`.nmap`, `.xml` and `.gnmap`) with the basename `tcpScan`.

If you found an open port, check that the service is really listening:

```sh
sudo nmap --script=rsync-list-modules 10.70.70.80 -p 873
```
