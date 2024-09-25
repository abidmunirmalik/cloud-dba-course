## CLOUD DATABAE ADMINISTRATION - RESET RDS INSTANCE

### RESET RDS REPLICA
```sql
show replica status\G
reset replica;
ERROR 1227 (42000): Access denied; you need (at least one of) the RDSADMIN USER privilege

show grants;
select user,host from mysql.user;

show grants for rdsadmin@localhost;
```

### RDS STORED PROCEDURE TO RESET RDS REPLICA
```sql
CALL mysql.rds_reset_external_master;
```

### CONFIGURE RDS REPLICA FROM EXTERNAL MASTER
```sql
CALL mysql.rds_set_external_master_with_auto_position (
  host_name
  , host_port
  , replication_user_name
  , replication_user_password
  , ssl_encryption
  , delay
);

CALL mysql.rds_set_external_master_with_auto_position ("144.126.217.88", 3306, "replication_admin", "P@ssw0rd123", 1, 0);
CALL mysql.rds_start_replication;
SHOW REPLICA STATUS\G
```
