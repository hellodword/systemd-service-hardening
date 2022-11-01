# systemd-service-hardening

## syscall

```sh
sudo strace -c ping 1.1.1.1 -c 1

sudo systemd-analyze syscall-filter

sudo systemd-analyze syscall-filter @privileged
```

```
SystemCallArchitectures=native
SystemCallFilter=@network-io
SystemCallFilter=setrlimit
```

> SystemCallLog

```sh
journalctl --since 13:11 --follow | grep SECCOMP | grep AdGuardHome | grep -oP '(?<=syscall=)\d+' > syscalls.txt

cat syscalls.txt | sort -n | uniq | xargs -L 1 ausyscall
```
