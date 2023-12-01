## CLOUD DBA COURSE -  SETUP EC2 AS REPLICA

### CLOUD REPLICA - PREPARE FOR REPLICATION
```sh
mkdir -p /var/log/mysql/binlogs && chown -R mysql:mysql /var/log/mysql/

vi /etc/my.cnf

# GTID-BASED Replication setup
server-id                  = 3
log-bin                    = /var/log/mysql/binlogs/cloud-replica-binlog
log-bin-index              = /var/log/mysql/binlogs/cloud-replica-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON
report-host                = cloud-replica.db.local

systemctl stop mysqld.service && systemctl start mysqld.service
mysql -u root -p
```

### CLOUD REPLICA - SETUP GTID-BASED REPLICATION
```sql
RESET REPLICA;
CHANGE REPLICATION SOURCE TO SOURCE_HOST='primary.db.local', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
SHOW REPLICA STATUS\G
```
