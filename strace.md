Trace only filei events (`-e file`) and also trace child processes as they are created by the currently traced processes (`-f`):
```
strace -e file -f myprogram
```
