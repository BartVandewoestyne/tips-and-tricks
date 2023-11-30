# iPerf

iPerf can be used to perform network throughput tests

Example iperf commands:
```
iperf3 --udp --client 10.177.0.2 --bitrate 5M --length 512
```

# Perf

Perf is a set of performance analysis tools for Linux.

## Recording data

First, record some data with `perf`.  To get backtraces, you will need to enable the `dwarf` callgraph mode:
```
sudo perf record --call-graph dwarf <your application>
```
The above command is for running `<your application>` under perf.  If you want to attach to a running process, do
```
sudo perf record --call-graph dwarf -p <pid-of-process>
```
This creates a `perf.tap.data` file which can be analyzed with `perf report` or hotspot.

## Analyzing with `perf report`

Simply in the directory where the `perf.data` file is present, do
```
perf report
```
or
```
perf report --symfs=<directory>
```
Sometimes, you also have to specify the `/proc/kallsyms` file:
```
perf report --kallsyms=/proc/kallsyms
```
where `/proc/kallsyms` is a file that exists since Linux 2.5.71 and holds the kernel exported symbol definitions used by the modules(X) tools to dynamically link and bind loadable modules.

To redirect the errors of `perf report` to a file (for further diagnosis):
```
perf report 2> error.log
```

References:
* https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/monitoring_and_managing_system_status_and_performance/recording-and-analyzing-performance-profiles-with-perf_monitoring-and-managing-system-status-and-performance

## Analyzing with Hotspot

In case you need another system root (e.g. from a Docker container):
```
sudo ./hotspot-v1.3.0-99-gdf39e78-x86_64.AppImage --sysroot=/var/lib/docker/overlay2/jfjkmfdjmdfsjklmfjkml/merged /media/bverstuyft/DATA/perf.tap.data
```
The `--sysroot` is the sysroot of the container that's being used.

If you get
```
Failed to parse kernel symbol mapping file ...
Module "[kernel.kallsyms]_text" is missing (some) debug symbols.
```
then add `--kallsyms=/proc/kallsyms` to the hotspot command.
Sometimes, you might also want to move your `/root/.debug` folder to another location (or clear it) to get your symbols visible.
