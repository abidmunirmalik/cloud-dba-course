## CLOUD DBA COURSE - Install MySQL Community Server


### INSTALL SPECIFIC MYSQL COMMUNITY SERVER
```sh
ssh -i ~/.ssh/cloud-db root@primary.db.local

sudo -i
cd /tmp
yum -y install wget
yum -y install tar

wget https://downloads.mysql.com/archives/get/p/23/file/mysql-8.0.35-1.el9.x86_64.rpm-bundle.tar
tar xvf mysql-8.0.35-1.el9.x86_64.rpm-bundle.tar


yum localinstall -y mysql-community-client-plugins-8.0.35-1.el9.x86_64.rpm
yum localinstall -y mysql-community-common-8.0.35-1.el9.x86_64.rpm
yum localinstall -y mysql-community-libs-8.0.35-1.el9.x86_64.rpm
yum localinstall -y mysql-community-icu-data-files-8.0.35-1.el9.x86_64.rpm
yum localinstall -y mysql-community-client-8.0.35-1.el9.x86_64.rpm
yum localinstall -y mysql-community-server-8.0.35-1.el9.x86_64.rpm

rpm -qa | grep mysql
systemctl enable mysqld.service && systemctl start mysqld.service
systemctl status mysqld.service
pidof mysqld
netstat -ntlp | grep 3306
```


### PERFORM SECURE INSTALLATION
```sh
grep "temporary password" /var/log/mysqld.log

mysql_secure_installation

mysql --host=localhost --user=root --password
mysql_config_editor set --user=root --password
```


### CREATE DBA & REPLICATION ADMIN USERS - PRIMARY ONLY
```sql
CREATE USER IF NOT EXISTS bob IDENTIFIED WITH BY 'P@ssw0rd123';
CREATE USER IF NOT EXISTS replication_admin IDENTIFIED BY 'P@ssw0rd123';
GRANT ALL PRIVILEGES ON *.* TO bob WITH GRANT OPTION;
GRANT REPLICATION SLAVE ON *.* TO replication_admin;
FLUSH PRIVILEGES;
```
