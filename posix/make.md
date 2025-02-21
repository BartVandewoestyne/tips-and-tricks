# make

## Dry-run

To write commands that would be executed on standard output, but not execute them (except in certain circumstances):

```bash
make -n [target_name...]
```

## Parallel execution

To set the maximum number of targets that can be updated concurrently:

```bash
make -j <maxjobs>
```
