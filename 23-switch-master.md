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
