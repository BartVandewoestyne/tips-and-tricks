# iPerf

Example iperf commands:
```
iperf3 --udp --client 10.177.0.2 --bitrate 5M --length 512
```

# Perf

The `perf` tool is under `/usr/bin/perf`.

```
bvandewoestyne@BVANDEW-70TZQ73:~$ perf --version
perf version 5.15.116
```

First, record some data with `perf`.  TO get backtraces, you will need to enable the dwarf callgraph mode:
```
sudo perf record --call-graph dwarf <your application>
```
or
```
sudo perf record --call-graph dwarf -p <pid-of-process>
```
This creates a perf.tap.data file which can be analyzed with hotspot.

# Hotspot

```
sudo ./hotspot-v1.3.0-99-gdf39e78-x86_64.AppImage --sysroot=/var/lib/docker/overlay2/jfjkmfdjmdfsjklmfjkml/merged /media/bverstuyft/DATA/perf.tap.data
```
The `--sysroot` is the sysroot of the container that's being used.
The above command opens hotspot, best to look at the flamegraph.
