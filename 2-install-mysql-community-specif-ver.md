## CLOUD DBA COURSE - Install MySQL Community Server


### INSTALL SPECIFIC MYSQL COMMUNITY SERVER
```sh
cd /tmp
wget https://downloads.mysql.com/archives/get/p/23/file/mysql-8.0.33-1.el7.x86_64.rpm-bundle.tar
tar xvf mysql-8.0.33-1.el7.x86_64.rpm-bundle.tar

yum localinstall -y mysql-community-client-plugins-8.0.33-1.el7.x86_64.rpm
yum localinstall -y mysql-community-common-8.0.33-1.el7.x86_64.rpm
yum localinstall -y mysql-community-libs-8.0.33-1.el7.x86_64.rpm
yum localinstall -y mysql-community-icu-data-files-8.0.33-1.el7.x86_64.rpm
yum localinstall -y mysql-community-client-8.0.33-1.el7.x86_64.rpm
yum localinstall -y mysql-community-server-8.0.33-1.el7.x86_64.rpm

rpm -qa | grep mysql

systemctl enable mysqld.service && systemctl start mysqld.service
systemctl status mysqld.service
pidof mysqld
netstat -ntlp | grep 3306
```

**Note:** Remove `mariadb-lib` only if you see following error
```sh
# yum localinstall -y mysql-community-libs-8.0.33-1.el7.x86_64.rpm
Error: Package: 2:postfix-2.10.1-6.amzn2.0.3.x86_64 (installed)
       Requires: libmysqlclient.so.18()(64bit)
       Removing: 1:mariadb-libs-5.5.68-1.amzn2.0.1.x86_64 (@amzn2-core)
           libmysqlclient.so.18()(64bit)

# yum remove -y mariadb-libs.x86_64
Removed:
  mariadb-libs.x86_64 1:5.5.68-1.amzn2.0.1
Dependency Removed:
  postfix.x86_64 2:2.10.1-6.amzn2.0.3
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
CREATE USER IF NOT EXISTS bob IDENTIFIED WITH mysql_native_password BY 'P@ssw0rd123';
CREATE USER IF NOT EXISTS replication_admin IDENTIFIED WITH mysql_native_password BY 'P@ssw0rd123';
GRANT ALL PRIVILEGES ON *.* TO bob WITH GRANT OPTION;
GRANT REPLICATION SLAVE ON *.* TO replication_admin;
FLUSH PRIVILEGES;
```
