## CLOUD DBA COURSE - SETUP RDS AS REPLICA

### RUN ON RDS INSTANCE
```sh
mysql -h prod.cquael8kyh30.us-east-1.rds.amazonaws.com -u admin -p

reset replica;

CALL mysql.rds_set_external_master_with_auto_position("144.126.217.88", 3306, "replication_admin","P@ssw0rd123", 1, 0);

CALL mysql.rds_start_replication;

SHOW REPLICA STATUS\G
```
