# GNU ps

To check how long a process has been running on Linux:

TODO: check if this is POSIX-compliant or not.

```text
ps -eo pid,etime,cmd | grep <process_name>
```

* `-e` Select all processes.  Identical to -A.
* `-o <format>` Specifiy the exact fields to display.
* `etime` shows the elapsed time since the process was started, in the form [[DD-]hh:]mm:ss..
