# POSIX commands

The standard is available here: https://pubs.opengroup.org/onlinepubs/9799919799/

## ls

To list all files with the last modified ones at the bottom:
```
ls -altr
```

## w

```
root@iDirectRMT:p6 ~ # w
USER		TTY		IDLE	TIME		 HOST
root            ttyS0           00:00   Nov 29 09:34:52
```

Here, ttyS0 means someone is logged in from the serial console 0.

## who

```
bvandewoestyne@RAPTOR-JUMPSERVER:~$ who
sweenah  pts/0        Nov 17 03:31 (10.250.220.39)
sharmila pts/2        Nov 28 22:21 (10.250.32.92)
parijat  pts/4        Nov 29 00:32 (10.250.52.14)
ppise    pts/5        Nov 29 01:51 (10.1.56.53)
bvandewoestyne pts/6        Nov 29 04:29 (10.60.30.239)
kponnusamy pts/7        Nov 27 08:39 (10.250.32.185)
ppise    pts/8        Nov 29 02:20 (10.1.56.58)
kponnusamy pts/9        Nov 28 07:38 (10.250.32.185)
bvandewoestyne pts/10       Nov 29 04:32 (10.60.30.239)
kponnusamy pts/14       Nov 28 07:45 (10.250.32.185)
kponnusamy pts/17       Nov 28 04:43 (10.250.32.185)
kponnusamy pts/18       Nov 28 07:46 (10.250.32.185)
kponnusamy pts/21       Nov 28 09:58 (10.250.32.185)
```
