Using nmap:
-----------

check for open ports:
  nmap -sSV -p- -oA tcpScan 10.70.70.83

if you found an open port, check that the service is really listening
  sudo nmap --script=rsync-list-modules 10.70.70.80 -p 873

In real time using TCPView:
---------------------------
https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview
