Listen on all interfaces:

```
tcpdump -i any
```

Capture only UDP traffic on eth0 and write to file
```
tcpdump -i eth0 -w capture.pcap udp
```

Capture ICMPv6 Router Advertisement messages (IPv6 address assignment):

```
tcpdump -i any -n -vv icmp6 and 'ip6[40]=134' -w capture.pcap
```

```
tcpdump -nvei any dst 10.100.104.102
```
* `-n`: Don't  convert  addresses  (i.e.,  host addresses, port numbers, etc.) to names.
* `-v`: When parsing and printing, produce (slightly more) verbose output.
* `-e`: Print  the  link-level  header  on  each dump line.

Info on what expressions can be used for tcpdump, see pcap-filter(7):
```
man pcap-filter
```
