# Routes

```
traceroute <ip-address>
```

# ARP

Viewing the ARP cache on your computer:
```
$ arp -n
```
or
```
$ cat /proc/net/arp
```

Clearing the ARP cache (preferred method):
```
sudo ip -s -s neigh flush all
```
References:
* https://linux-audit.com/how-to-clear-the-arp-cache-on-linux/

Creating static arp addresses?
```
arp -s 192.168.5.2 <some mac address>
```

# Linux Network Namespaces

## Creating and listing network namespaces

Create a new network namespace on a Linux host:
```
ip netns add red
```

List network namespaces:
```
ip netns
```

To list the interfaces or show the arp or routing table on my host:
```
$ ip link
$ arp
$ route
```

To execute the `ip link` command inside the `red` namespace:
```
ip netns exec red ip link
ip netns exec red arp
ip netns exec red route
```
or
```
ip -n red link
```

## Establishing connectivity

Create 'virtual ethernet pair' or 'pipe':
```
ip link add veth-red type veth peer name veth-blue
```
Now the virtual ethernet interfaces `veth-red` and `veth-blue` must still be attached to the appropriate namespace:
```
ip link set veth-red netns red
ip link set veth-blue netns blue
```
Now we can assign IP addresses to each of these namespaces:
```
ip -n red  addr add 192.168.15.1 dev veth-red
ip -n blue addr add 192.168.15.2 dev veth-blue
```
Then bring interfaces up:
```
ip -n red  link set veth-red up
ip -n blue link set veth-red up
```

Now you can ping and arp from red or blue:
```
ip netns exec red ping 192.168.15.2
ip netns exec red arp
ip netns exec blue arp
```
Note that the `arp` table on the host does not see any of this.

# Create virtual switch

For more than two hosts, use a virtual switch.
You can use 'Linux bridge' or 'OVS Open vSwitch'.

Using 'Linux brigde', to create an internal bridge network, we add a new interface to the host using the following `ip link add` command with type set to `bridge`:
```
ip link add v-net-0 type bridge
```
For our host, this is just another interface which appears in the output of the `ip link` command.
And bring it up with:
```
ip link set dev v-net-0 up
```

To delete virtual cable:
```
ip -n red link del veth-red
```
Note that deleting one end deletes the other end automatically.

Now create cables:
```
ip link add veth-red  type veth peer name veth-red-br
ip link add veth-blue type veth peer name veth-blue-br
ip link set veth-red netns red
ip link set veth-red-br master v-net-0
ip link set veth-blue netns blue
ip link set veth-blue-br master v-net-0
```

Now set ip addresses:
```
ip -n red  addr add 192.168.15.1 dev veth-red
ip -n blue addr add 192.168.15.2 dev veth-blue
```
and bring up
```
ip -n red  link set veth-red  up
ip -n blue link set veth-blue up
```

Now set IP address of bridge:
```
ip addr add 192.168.15.5/24 dev v-net-0
```
Then you can ping from your localhost:
```
ping 192.168.15.1
```

Route all traffic:
```
ip netns exec blue ip route add 192.168.1.0/24 via 192.168.15.5
```

Now NAT:
```
iptables -t nat -A POSTROUTING -s 192.168.15.0/24 -j MASQUERADE
```
Add default gw:
```
ip netns exec blue ip route add default via 192.168.15.5
```

References:
  * https://www.youtube.com/watch?v=j_UUnlVC2Ss

# netcat

Start listening somewhere:
```
nc -u -l 9999
```
Then connect:
```
nc -u 10.177.0.2 9999
```
and now start typing to see data appearing on the other end.
