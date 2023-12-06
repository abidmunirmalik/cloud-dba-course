## CLOUD DBA COURSE - BACKUP TO S3 BUCKET

### STOP MYSQL ON CLOUD-REPLICA EC2
```sql
SHOW REPLICA STATUS;
SET GLOBAL innodb_fast_shutdown = 0;
STOP REPLICA;
sudo systemctl stop mysqld.service
```


### COPY BACKUP TO S3
```sh
sudo chown -R ec2-user:ec2-user /var/lib/mysql
aws s3 cp /var/lib/mysql s3://golddataprotectors/backups/full_backup --recursive
sudo chown -R mysql:mysql /var/lib/mysql
```

### START MYSQL ON CLOUD-REPLICA EC2
```sql
sudo systemctl start mysqld.service
START REPLICA;
SHOW REPLICA STATUS\G;
```
