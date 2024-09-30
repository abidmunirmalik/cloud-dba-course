## CLOUD DATABAE ADMINISTRATION - CUTOVER TO RDS



### ON PRIMARY
```sql
FLUSH TABLES WITH READ LOCK;
SET GLOBAL read_only=TRUE;
SET GLOBAL event_scheduler='OFF';
systemctl stop mysqld.service 
```


#### POINT YOUR APPLICATION TO RDS
* Change the CNAME pointing on-prem Primary to RDS
* Example:
  * prod --> primary.db.local
  * prod --> prod.cquael8kyh30.us-east-1.rds.amazonaws.com



### ON RDS
```sql
SHOW REPLICA STATUS\G
CALL mysql.rds_stop_replication;
CALL mysql.rds_reset_external_master;

SHOW PROCESSLIST;
SHOW REPLICAS;
SHOW MASTER STATUS;

SELECT * FROM information_schema.processlist WHERE command <> 'Sleep' ORDER BY  time DESC;

SELECT user,sum(CURRENT_CONNECTIONS) FROM performance_schema.accounts  
GROUP BY user 
HAVING SUM(CURRENT_CONNECTIONS)>0 
ORDER BY  SUM(CURRENT_CONNECTIONS) DESC;
```
