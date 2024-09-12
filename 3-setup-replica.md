## CLOUD DBA COURSE - Setup On-Prem Replica with GTID-Based Replication


### REPLICA - PREPARE FOR BACKUP RESTORE
```sh
systemctl stop mysqld.service && rm -rf /var/lib/mysql/*
```

### PRIMARY - PREPARE FOR REPLICATION
```sh
systemctl stop mysqld.service

vi on-prem (copy this file contents from your local ~/.ssh/on-prem file)
chmod 600 on-prem

scp -i on-prem -r /var/lib/mysql/* root@replica.db.local:/var/lib/mysql/

mkdir -p /var/log/mysql/binlogs && chown -R mysql:mysql /var/log/mysql/

vi /etc/my.cnf

# GTID-BASED Replication setup
server-id                  = 1
log-bin                    = /var/log/mysql/binlogs/primary-binlog
log-bin-index              = /var/log/mysql/binlogs/primary-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON

systemctl start mysqld.service
```

### REPLICA - PREPARE FOR REPLICATION
```sh
rm -f /var/lib/mysql/auto.cnf && rm -f /var/lib/mysql/binlog.* && rm -f /var/lib/mysql/undo_*

chown -R mysql:mysql /var/lib/mysql

mkdir -p /var/log/mysql/binlogs && chown -R mysql:mysql /var/log/mysql/

vi /etc/my.cnf
# GTID-BASED Replication setup
server-id                  = 2
log-bin                    = /var/log/mysql/binlogs/replica-binlog
log-bin-index              = /var/log/mysql/binlogs/replica-binlog.index
binlog-expire-logs-seconds = 432000
gtid-mode                  = ON
enforce-gtid-consistency   = ON
report-host                = replica.db.local

systemctl stop mysqld.service && systemctl start mysqld.service
mysql -u root -p
```

### REPLICA - SETUP GTID-BASED REPLICATION
```sql
CHANGE REPLICATION SOURCE TO SOURCE_HOST='primary.db.local', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
SHOW REPLICA STATUS;
```

### REPLICATION ERROR - CASHING_SHA2_PASSWORD REQUIRES SECURE CONNECTION
```sh
Last_IO_Error: Error connecting to source 'replication_admin@primary.db.local:3306'. This was attempt 3/86400, with a delay of 60 seconds between attempts. Message: Authentication plugin 'caching_sha2_password' reported error: Authentication requires secure connection.

STOP REPLICA;
SELECT user, host, plugin FROM mysql.user WHERE user LIKE 'replication%';
ALTER USER replication_admin IDENTIFIED WITH mysql_native_password BY 'P@ssw0rd123'; (Both Primary & Replica)
Restart Primary mysqld i.e systemctl start mysqld && systemctl start mysqld
START REPLICA;
SHOW REPLICA STATUS\G
```

### TESTING REPLICATION
```sql
CREATE DATABASE employees;
USE employees;
CREATE TABLE employee(emp_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, emp_fname VARCHAR(25) NOT NULL, emp_lname VARCHAR(25) NOT NULL);
INSERT INTO employee(emp_fname, emp_lname)
VALUES
 ('Bobby', 'Muller'),
 ('Prasad', 'Kumar'),
 ('Tom', 'Brady'),
 ('Johny', 'Doe'),
 ('Josh', 'Middleton');
```

