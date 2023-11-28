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
