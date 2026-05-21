# Process commands and their outputs:
## ps-
      1)yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar$ ps
          PID TTY          TIME CMD
          362 pts/0    00:00:00 bash
          898 pts/0    00:00:00 ps

## top-
     2)top - 17:12:28 up 7 min,  1 user,  load average: 0.01, 0.07, 0.05
          Tasks:  35 total,   1 running,  34 sleeping,   0 stopped,   0 zombie
          %Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
          MiB Mem :   3830.2 total,   2411.8 free,    503.3 used,   1058.9 buff/cache
          MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   3326.9 avail Mem
          
              PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
             1391 yogesh_+  20   0    9400   5632   3456 R   0.3   0.1   0:00.01 top
                1 root      20   0   21848  12160   9216 S   0.0   0.3   0:01.45 systemd
                2 root      20   0    3120   1920   1920 S   0.0   0.0   0:00.02 init-systemd(Ub
                6 root      20   0    3120   1792   1792 S   0.0   0.0   0:00.00 init
               42 root      19  -1   66752  14808  14040 S   0.0   0.4   0:00.34 systemd-journal

# Service commands
## Systemctl status-

        1)yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar$ systemctl status nginx
        ● nginx.service - A high performance web server and a reverse proxy server
             Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
             Active: active (running) since Fri 2026-04-24 17:05:02 UTC; 10min ago
               Docs: man:nginx(8)
            Process: 168 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
            Process: 189 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
           Main PID: 194 (nginx)
              Tasks: 9 (limit: 4584)
             Memory: 7.6M (peak: 7.9M)
                CPU: 118ms
             CGroup: /system.slice/nginx.service
                     ├─194 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
                     ├─195 "nginx: worker process"
                     ├─196 "nginx: worker process"
                     ├─197 "nginx: worker process"
                     ├─198 "nginx: worker process"
                     ├─199 "nginx: worker process"
                     ├─200 "nginx: worker process"
                     ├─201 "nginx: worker process"
                     └─202 "nginx: worker process"
## Systemctl list-units-
          yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar$ systemctl list-units
          UNIT                                                                                                                                                                         LOAD   ACTIVE     SUB          DE>
          sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-MSFT1000:00-c4b741f5\x2d5582\x2d4c98\x2d8f8b\x2d2e082933c396-pci5582:00-5582:00:00.0-virtio0-virtio\x2dports-vport0p0.device loaded active     plugged      /s>
          sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-MSFT1000:00-c4b741f5\x2d5582\x2d4c98\x2d8f8b\x2d2e082933c396-pci5582:00-5582:00:00.0-virtio0-virtio\x2dports-vport0p1.device loaded active     plugged      /s>
          sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-MSFT1000:00-c4b741f5\x2d5582\x2d4c98\x2d8f8b\x2d2e082933c396-pci5582:00-5582:00:00.0-virtio0-virtio\x2dports-vport0p2.device loaded active     plugged      /s>
          sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-MSFT1000:00-eef38dee\x2dfbad\x2d47e1\x2d9e30\x2dd1155bc51a1a-net-eth0.device                                                 loaded active     plugged      /s>

# LOG commands:
## Logs for units(e.gn nginx)

        yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar$ journalctl -u nginx
        Apr 20 17:44:05 Profound systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
        Apr 20 17:44:05 Profound systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
        Apr 20 17:50:15 Profound systemd[1]: Stopping nginx.service - A high performance web server and a reverse proxy server...
        Apr 20 17:50:15 Profound systemd[1]: nginx.service: Deactivated successfully.
        Apr 20 17:50:15 Profound systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy server.
## System logs from /var/log

        yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar$ head /var/log/syslog
        2026-04-20T04:27:38.038913+00:00 Profound systemd[1]: Mounted dev-hugepages.mount - Huge Pages File System.
        2026-04-20T04:27:38.039831+00:00 Profound systemd[1]: Mounted dev-mqueue.mount - POSIX Message Queue File System.
        2026-04-20T04:27:38.039853+00:00 Profound systemd[1]: Mounted sys-kernel-debug.mount - Kernel Debug File System.
        2026-04-20T04:27:38.039859+00:00 Profound systemd[1]: Mounted sys-kernel-tracing.mount - Kernel Trace File System.
        2026-04-20T04:27:38.039863+00:00 Profound systemd[1]: Finished keyboard-setup.service - Set the console keyboard layout.
        2026-04-20T04:27:38.039868+00:00 Profound systemd[1]: Finished kmod-static-nodes.service - Create List of Static Device Nodes.
        2026-04-20T04:27:38.039872+00:00 Profound systemd[1]: modprobe@configfs.service: Deactivated successfully.
        2026-04-20T04:27:38.039877+00:00 Profound systemd[1]: Finished modprobe@configfs.service - Load Kernel Module configfs.
        2026-04-20T04:27:38.039745+00:00 Profound kernel: Linux version 6.6.87.2-microsoft-standard-WSL2 (root@439a258ad544) (gcc (GCC) 11.2.0, GNU ld (GNU Binutils) 2.37) #1 SMP PREEMPT_DYNAMIC Thu Jun  5 18:30:46 UTC 2025
        2026-04-20T04:27:38.040046+00:00 Profound kernel: Command line: initrd=\initrd.img WSL_ROOT_INIT=1 panic=-1 nr_cpus=8 hv_utils.timesync_implicit=1 console=hvc0 debug pty.legacy_count=0 WSL_ENABLE_CRASH_DUMP=
      
      
      
      
      
      
      
      
      
      
      
        
