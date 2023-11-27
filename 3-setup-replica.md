## CLOUD DBA COURSE - Setup On-Prem Replica with GTID-Based Replication


### REPLICA - PREPARE FOR BACKUP RESTORE
```sh
systemctl stop mysqld.service && rm -rf /var/lib/mysql/*
```

### PRIMARY - PREPARE FOR REPLICATION
```sh
systemctl stop mysqld.service
scp -i cloud-db -r /var/lib/mysql/* root@replica.db.local:/var/lib/mysql/

vi /etc/my.cnf
log-bin                    = /var/log/mysql/binlogs/primary-binlog
log-bin-index              = /var/log/mysql/binlogs/primary-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON

systemctl start mysqld.service
```

### REPLICA - PREPARE FOR REPLICATION
```sh
rm -f /var/lib/mysql/*.auto && rm -f /var/lib/mysql/iblogs*
chown -R mysql:mysql /var/lib/mysql && systemctl start mysqld.service

mkdir -p /var/log/mysql/binlogs && chown -R mysql:mysql /var/log/mysql/
vi /etc/my.cnf
server-id                  = 2
log-bin                    = /var/log/mysql/binlogs/replica-binlog
log-bin-index              = /var/log/mysql/binlogs/replica-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON
report-host                = replica.db.local

systemctl stop mysqld.service && systemctl start mysqld.service
```

### REPLICA - SETUP GTID-BASED REPLICATION
```sql
CHANGE REPLICATION SOURCE TO SOURCE_HOST='primary.db.local', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
SHOW REPLICA STATUS;
```
