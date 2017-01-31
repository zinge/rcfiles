### Get and install 
first go postgresql site and find information about repo, https://www.postgresql.org/download/linux/debian/

use repo for 9.6 postgresql
after install repo,
list available distros, i'm  use 
```
#echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" >> /etc/apt/sources.list

$wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
  sudo apt-key add -
$sudo apt-get update
```
and install 
```
$sudo apt-get install postgresql-9.6 postgresql-client-9.6
```

### Enable autostart and first start service
```
$sudo systemctl list-unit-files | grep postgresql
```
### Tune postgresql.conf
Okay, after start server a look memmory and CPU usage ... damn ...

Tune postgresql.conf file, from 512MB memory usage, and 5 connections, with http://pgtune.leopard.in.ua/
```
max_connections = 5
effective_cache_size = 384MB
work_mem = 26214kB
maintenance_work_mem = 32MB
min_wal_size = 1GB
max_wal_size = 2GB
checkpoint_completion_target = 0.7
wal_buffers = 3932kB
shared_buffers = 128MB
default_statistics_target = 100
```
