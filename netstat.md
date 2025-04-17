# netstat

Note: Use `ss` instead of `netstat` for faster, modern output!

## On Windows and Linux

```text
netstat -an
```

* display all active TCP connections and the TCP and UDP ports on which the computer is listening,
* express addresses and port numbers numerically and do not attempt to determine namems

## On Windows

```text
netstat -an 1 | find "4444"
```

```text
netstat -an 1 | find "4444" | find "ESTABLISHED"
```

```text
netstat -ano 1 | find "Dest_IP_Addr"
```

## On Linux

Show only TCP connections:

```sh
netstat -at
```

Show only UDP connections:

```sh
netstat -au
```

Show listening ports only:

```sh
netstat -l
```

Show process PID with connections:

```sh
netstat -tulnp
```

Show kernel routing table (like `route -n`):

```sh
netstat -r
```

View interface statistics:

```sh
netstat -i
```

## References

* [Wikipedia - netstat](https://en.wikipedia.org/wiki/Netstat)
* [Windows Server - netstat documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/netstat)
