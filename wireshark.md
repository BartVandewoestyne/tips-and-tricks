# Tips

* To be able to capture loopback traffic:
  -> Make sure you don't have WinPcap installed.
  -> Make sure your install Wireshark with NpCap, not in WinPcap compatibility
     mode.
  -> It can be that you have to select another 'Ethernet X' adapter instead of
     the 'Npcap Loopback Adapter' in order to see traffic on 127.0.0/8 hosts.
     
* With tcpreplay you can replay network traffic captured with tcpdump or Wireshark: https://github.com/appneta/tcpreplay

* It is possible to enable or disable the UDP checksum in Wireshark.  TODO: how?

# Useful capture filters:

* Filter based on IP:

    ip.addr == 10.0.0.145
    ip.src == 10.0.0.145
    ip.dst == 10.0.0.145

* To see only certain protocols:

    arp
    tcp
    dns
    http
    dns or http

* TCP or UDP port number:

    tcp.port == 443  (either src or dst port)
    udp.port == 443  (either src or dst port)

* Show any TCP problems:

    tcp.analysis.flags

* Remove noise:

    !(arp or dns or icmp)

* Follow TCP stream (1 single connection)o
  -> select any packet -> Follow tcp stream

* To see TCP or UDP packets that contain a certain string:

    tcp contains foobar
    udp contains foobar

* Display all HTTP requests:

    http.request

* Display specific HTTP responses:

    http.response.code == 200

* Is one of my server being SYN attacked?

    tcp.flags.syn == 1

* Show all tcp resets

    tcp.flags.reset == 1

* VoIP

    sip
    rtp
    sip && rtp

* To see TCP or UDP packets that match a certain string:

    tcp matches "foo.*bar"
    udp matches "foo.*bar"
