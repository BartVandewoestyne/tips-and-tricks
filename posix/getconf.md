# getconf

## Number of processors

To get the 'Maximum number of execution units currently available to run threads' (with the remark that the nature of an execution unit and the precise conditions under which an execution unit is considered to be available, or can be made available, or how many threads it can execute in parallel, are implementation-defined):

```text
getconf _NPROCESSORS_ONLN
```
