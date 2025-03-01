```
# zfs get direct tpool
NAME            PROPERTY  VALUE     SOURCE
tpool           direct    standard  local

# dd if=/dev/zero of=test.file bs=1M count=1M status=progress 
12870221824 bytes (13 GB, 12 GiB) copied, 6 s, 2.1 GB/s ^C
12983+0 records in
12983+0 records out
13613662208 bytes (14 GB, 13 GiB) copied, 6.31836 s, 2.2 GB/s

# dd if=/dev/zero of=test.file bs=1M count=1M status=progress oflag=direct
16501440512 bytes (17 GB, 15 GiB) copied, 6 s, 2.8 GB/s^C
16408+0 records in
16408+0 records out
17205035008 bytes (17 GB, 16 GiB) copied, 6.25873 s, 2.7 GB/s
```
