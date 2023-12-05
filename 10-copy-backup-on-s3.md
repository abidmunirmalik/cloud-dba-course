## CLOUD DBA COURSE -  COPY BACKUP TO S3 BUCKET

### COPY EC2 COLD BACKUP TO S3 BUCKET
```sql
SET GLOBAL innodb_shutdown_fast = 0;
STOP REPLICA;
systemctl stop mysqld.service
```


### USING AWS CLI S3API
```sh
aws s3api list-buckets
aws s3api create-bucket --bucket golddataprotector --region us-east-1
aws s3api put-object --bucket golddataprotector --key backups/
aws s3api put-object --bucket golddataprotector --key backups/full_backup/world/countries.ibd
aws s3api list-objects --bucket golddataprotector --query "Contents[].{Key: Key}" --output text | while read -r line; do aws s3api delete-object --bucket golddataprotector --key "$line"; done
aws s3api put-object --bucket golddataprotectors --key backups/full_backup
aws s3api get-bucket-policy --bucket my-bucket
aws s3api get-bucket-acl --bucket my-bucket
```
