## CLOUD DBA COURSE - Restore Cold Backup on EC2

### EC2 - SHUTDOWN MYSQLD & REMOVE DATA DIRECTORY
```sh
mkdir /tmp/restore
sudo -i
systemctl stop mysqld && rm -rf /var/lib/mysql/*
```

### ON-PREM REPLICA - COLD BACKUP
```sh
mysql> SET GLOBAL innodb_fast_shutdown = 0;
mysql> stop replica;
systemctl stop mysqld

vi ec2-cloud-db.pem
chmod 600 ec2-cloud-db.pem

vi /etc/hosts
12.34.567.789 cloud-replica.db.local cloud-replica
scp -i ec2-cloud-db.pem -r /var/lib/mysql/* ec2-user@cloud-replica.db.local:/tmp/restore
```

### EC2 - RESTORE COLD BACKUP
```sh
sudo -i
rm -f /tmp/restore/auto.cnf && rm -f /tmp/restore/binlog.* && rm -f /tmp/restore/replica-relay-bin.*
cp -r /tmp/restore/* /var/lib/mysql/
chown -R mysql:mysql /var/lib/mysql


vi /etc/my.cnf
server-id = 3

systemctl start mysqld.service
pidof mysqld
```
