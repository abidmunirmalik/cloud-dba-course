## CLOUD DBA COURSE -  SETUP EC2 AS REPLICA

### CLOUD REPLICA - PREPARE FOR REPLICATION
```sh
mkdir -p /var/log/mysql/binlogs
chown -R mysql:mysql /var/log/mysql/

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

vi /etc/hosts
12.345.678.910  primary.db.local primary
111.122.444.555  replica.db.local replica

mysql -h primary.db.local -u replication_admin -p
```

### CLOUD REPLICA - SETUP GTID-BASED REPLICATION
```sql
mysql -u root -p
RESET REPLICA;
CHANGE REPLICATION SOURCE TO SOURCE_HOST='primary.db.local', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
SHOW REPLICA STATUS\G
```
