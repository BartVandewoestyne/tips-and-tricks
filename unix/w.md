# w

The command w on many Unix-like operating systems provides a quick summary of every user logged into a computer, what each user is currently doing, and what load all the activity is imposing on the computer itself.

Example from my laptop:

```text
bvandewoestyne@BVANDEW-70TZQ73:~$ w
 14:49:09 up 16:58,  1 user,  load average: 0,67, 0,88, 0,90
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
bvandewo :0       :0                Di21   ?xdm?   3:50m  0.00s /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --systemd --session=ubuntu
```

Example from a iDirect modem:

```text
root@iDirectRMT:p6 ~ # w
USER        TTY     IDLE    TIME         HOST
root            ttyS0           00:00   Nov 29 09:34:52
```

Example from the `eng4` server:

```text
newtec@eng4:~$ w
 13:56:10 up 415 days,  5:53,  5 users,  load average: 0.91, 1.31, 1.24
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
newtec   pts/0    10.60.90.106     02Jan25 33days  0.15s  0.15s -bash
newtec   pts/1    10.60.90.106     Mon10    2days  0.46s  0.46s -bash
newtec   pts/2    10.60.90.106     Tue06   31:00m  3:17m  0.24s -bash
newtec   pts/3    10.60.90.106     Tue07   23:56m  1.84s  0.00s sleep 100
newtec   pts/4    10.60.36.33      11:13    2.00s  0.18s  0.02s w
```

* `ttyS0` means someone is logged in from the serial console 0.
* `pts/0` refers to a pseudo-terminal slave (PTS), which is a virtual terminal used for remote or GUI-based shell sessions.  It typically appears when a user logs in via SSH, a terminal emulator (e.g. `gnome-terminal` or `xterm`) or another remote session.  The `/0` part indicates the terminal session number.  If multiple sessions exist,  you might see `pts/1`, `pts/2`, etc.

## References

* <https://en.wikipedia.org/wiki/W_(Unix)>
