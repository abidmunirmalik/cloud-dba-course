## CLOUD DBA COURSE - SETUP RDS FROM S3 BACKUP

### REMOVE UNWANTED FILES FROM S3 BUCKET
```sh
aws s3 ls s3://golddataprotectors
aws s3 ls s3://golddataprotectors/backups/full_backup/
aws s3api delete-object --bucket golddataprotectors --key backups/full_backup/auto.cnf
aws s3api delete-object --bucket golddataprotectors --key backups/full_backup/binlog.index
aws s3api delete-object --bucket golddataprotectors --key backups/full_backup/ip-172-31-41-33-relay-bin.000002
```

### CREATE IAM ROLE & SECURITY GROUP
```sh
Security Group Name: rds-sg
inbound: 3306 from internet

IAM Role: RDS-To-S3
permissions: ReadOnlyS3
```

### CREATE RDS FROM S3 BUCKET BACKUP
```sh
S3 bucket: golddataprotectors
S3 prefix: backups/full_backup
Engine: MySQL
Edition: MySQL Community
Source Engine Version: 8.0
Engine Version: 8.0.33
IAM Role: RDS-To-S3
DB Instance Class: db.t2.small
DB instance identifier: rds-gdp-db
Master username: admin
Password: XXX
Storage type: gp3
Size: 20GB
uncheck Enable storage autoscaling
Availability & Durability: Do not create a standby instance
Network Type: IPv4
VPC: default
DB subnet group: default-vpc
Public Access: yes
Security Group: rds-sg
Availability Zone: No Preference
Database authentication: Password authentication
Backup:
Uncheck Enable automated backups
Encryption:
Uncheck Enable encryption
Uncheck Enable Enhanced monitoring
Maintenance:
Uncheck Enable auto minor version upgrade
Delete Protection:
Uncheck Enable deletion protection
```
