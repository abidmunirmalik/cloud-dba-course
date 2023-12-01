## CLOUD DBA COURSE - Restore Cold Backup on EC2

### EC2 - SHUTDOWN MYSQLD & REMOVE DATA DIRECTORY
```sh
ssh -i "aws-ec2" ec2-user@ec2-12-34-567-789.compute-1.amazonaws.com
sudo systemctl stop mysqld && sudo rm -rf /var/lib/mysql/* && mkdir /tmp/restore
```

### ON-PREM REPLICA - COLD BACKUP
```sh
mysql> SET GLOBAL innodb_fast_shutdown = 0;
mysql> stop replica;
systemctl stop mysqld
vi aws-ec2
chmod 600 aws-ec2
vi /etc/hosts
12.34.567.789 cloud-replica.db.local
scp -i aws-ec2 -r /var/lib/mysql/* ec2-user@cloud-replica.db.local:/tmp/restore
```

### EC2 - RESTORE COLD BACKUP
```sh
sudo -i
cp -r /tmp/restore/* /var/lib/mysql/
chown -R mysql:mysql /var/lib/mysql
rm -f /var/lib/mysql/auto.cnf && rm -f /var/lib/mysql/binlog.* && rm -f /var/lib/mysql/replica-relay-bin.*

vi /etc/my.cnf
server-id = 3

systemctl start mysqld.service
```
