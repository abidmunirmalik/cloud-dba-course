## CLOUD DATABAE ADMINISTRATION - MYSQL MINOR VERSION UPGRADE


### ON REPLICA
```sql
STOP REPLICA;
systemctl stop mysqld.service

cp /etc/my.cnf /tmp/my.cnf
cd /tmp
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.39-1.el9.x86_64.rpm-bundle.tar
tar xvf mysql-8.0.39-1.el9.x86_64.rpm-bundle.tar

rpm -qa | grep mysql
yum -y remove mysql-community-server-8.0.35-1.el9.x86_64
yum -y remove mysql-community-client-8.0.35-1.el9.x86_64
yum -y remove mysql-community-icu-data-files-8.0.35-1.el9.x86_64
yum -y remove mysql-community-libs-8.0.35-1.el9.x86_64
yum -y remove mysql-community-client-plugins-8.0.35-1.el9.x86_64
yum -y remove mysql-community-common-8.0.35-1.el9.x86_64

yum -y localinstall mysql-community-client-plugins-8.0.39-1.el9.x86_64.rpm
yum -y localinstall mysql-community-common-8.0.39-1.el9.x86_64.rpm
yum -y localinstall mysql-community-libs-8.0.39-1.el9.x86_64.rpm
yum -y localinstall mysql-community-icu-data-files-8.0.39-1.el9.x86_64.rpm
yum -y localinstall mysql-community-client-8.0.39-1.el9.x86_64.rpm
yum -y localinstall mysql-community-server-8.0.39-1.el9.x86_64.rpm

rpm -qa | grep mysql
vi /etc/my.cnf

rm -f /etc/my.cnf
cp /tmp/my.cnf /etc/my.cnf

systemctl start mysqld.service && systemctl status mysqld.service
```



### ON RDS
```sql
SHOW REPLICAS;
```
