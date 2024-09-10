## CLOUD DBA COURSE - Install MySQL Community Server


### INSTALL SPECIFIC MYSQL COMMUNITY SERVER ON EC2
```sh
cp ~/Downloads/ec2-cloud-db.pem ~/.ssh/
chmod 400 ~/.ssh/ec2-cloud-db.pem
ssh -i ~/.ssh/ec2-cloud-db.pem ec2-user@ec2-3-90-163-76.compute-1.amazonaws.com
sudo -i
yum -y install wget tar
cd /tmp
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
