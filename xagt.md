If you notice that the `xagt` process is giving a high CPU load (sometimes >70 or even 90%), you can edit `/usr/lib/systemd/system/xagt.service` and add `CPUQuota=10%` to the `[Service]` section.
