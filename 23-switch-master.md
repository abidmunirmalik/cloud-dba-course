## CLOUD DATABAE ADMINISTRATION - SWITCH MASTER


AWS Documentation Reference: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/mysql-stored-proc-configuring.html

### ON RDS
```sql
CALL mysql.rds_show_configuration;
CALL mysql.rds_set_configuration('binlog retention hours', 120);
```

### ON ON-PREM REPLICA
```sql
stop replica;
show replica status\G
```

### ON PRIMARY
```sql
INSERT INTO employees.employee(emp_fname, emp_lname) VALUES ('Johny', 'Walker');
```

### ON RDS
```sql
SHOW REPLICA STATUS\G
CALL mysql.rds_stop_replication;
SHOW BINARY LOGS;
SHOW MASTER STATUS;
```

### ON ON-PREM REPLICA
```sql
CHANGE REPLICATION SOURCE TO SOURCE_HOST='prod.cquael8kyh30.us-east-1.rds.amazonaws.com', SOURCE_USER='replication_admin', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_AUTO_POSITION=1;
START REPLICA;
SHOW REPLICA STATUS\G
```

### ON-PREP REPLICA ERROR FIXING
```sql
Last_IO_Error: Got fatal error 1236 from source when reading data from binary log: 'Cannot replicate because the source purged required binary logs. Replicate the missing transactions from elsewhere, or provision a new replica from backup. Consider increasing the source's binary log expiration period. The GTID set sent by the replica is '2369c7ab-7062-11ef-8721-9a11dc327157:1-10,
eed026bb-70b9-11ef-9e16-763f7d99bd59:1', and the missing transactions are '86ce3761-75d1-11ef-b870-0e21c19f098f:1-3077''


CHANGE REPLICATION FILTER REPLICATE_WILD_IGNORE_TABLE=('innodb_memcache.%', 'mysql.rds_%', 'performance_schema.%');
show global variables like 'gtid_purged';
set global gtid_purged='86ce3761-75d1-11ef-b870-0e21c19f098f:1-3083';
start replica;
show replica status\G

vi /etc/my.cnf
replicate_wild_ignore_table=mysql.rds%, innodb_memcache.%, performance_schema.%

systemctl stop mysqld && systemctl start mysqld
start replica;
show replica status\G
```
