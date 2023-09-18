Listen on all interfaces:

```
tcpdump -i any
```

Capture ICMPv6 Router Advertisement messages (IPv6 address assignment):

```
tcpdump -i any -n -vv icmp6 and 'ip6[40]=134' -w capture.pcap
```

TODO: check what this exactly does:
```
tcpdump -nvei any dst 10.100.104.102
```
