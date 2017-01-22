### Get and install 
firs go postgresql site and find information about repo, https://yum.postgresql.org/repopackages.php
use repo for 9.6 postgresql
after install repo,
list available distros, i'm  use 
```
yum list postgresql*
```
and install 
```
$sudo yum install postgresql96 postgresql96-server pgadmin3_96
```

### Enable autostart and first start service
```
systemctl list-unit-files | grep postgresql
```
look at available systemd service file, enable and start this(
  initialize DB first 
```
$sudo /usr/pgsql-9.6/bin/postgresql96-setup initdb
```
### Tune postgresql.conf
Okay, after start server a look memmory and CPU usage ... damn ...
Tune postgresql.conf file, from 1GB memory usage, and 10 connections, with http://pgtune.leopard.in.ua/
```
max_connections = 10
shared_buffers = 256MB
effective_cache_size = 768MB
work_mem = 26214kB
maintenance_work_mem = 64MB
min_wal_size = 1GB
max_wal_size = 2GB
checkpoint_completion_target = 0.7
wal_buffers = 7864kB
default_statistics_target = 100
```
