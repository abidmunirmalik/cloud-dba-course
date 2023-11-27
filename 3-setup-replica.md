## CLOUD DBA COURSE - Setup Replica


### COPY COLD BACKUP FROM PRIMARY TO REPLICA
```sh
systemctl stop mysqld.service (Primary & Replica)
rm -rf /var/lib/mysql/* (Replica)
scp -r /var/lib/mysql/* root@replica.db.local:/var/lib/mysql/ (Primary)
chown -R mysql:mysql /var/lib/mysql (Replica)
systemctl start mysqld.service (Replica)
mysql_config_editor set --user=bob --password (Replica)
mysql
```

### PREPARE FOR GTID-BASED REPLICATION
```sh
vi /etc/my.cnf (Replica)
server-id                  = 2
systemctl stop mysqld.service && systemctl start mysqld.service
mysql
show global variables like 'server_id';

mkdir -p /var/log/mysql/binlogs
chown -R mysql:mysql /var/log/mysql/binlogs

vi /etc/my.cnf (Primary)
log-bin                    = /var/log/mysql/binlogs/primary-binlog
log-bin-index              = /var/log/mysql/binlogs/primary-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON

vi /etc/my.cnf (Replica)
log-bin                    = /var/log/mysql/binlogs/replica-binlog
log-bin-index              = /var/log/mysql/binlogs/replica-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON
```

### SETUP GTID-BASED REPLICATION
```sql
CHANGE REPLICATION SOURCE TO SOURCE_HOST='primary.db.local', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
```
