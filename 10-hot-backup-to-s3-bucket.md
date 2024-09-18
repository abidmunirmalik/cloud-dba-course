## CLOUD DBA COURSE - HOT BACKUP TO S3 BUCKET

### COPY HOT BACKUP TO S3
```sh
aws s3 ls s3://golddataprotectors/backups/
cd /tmp
aws s3 cp --recursive hot_backup 
aws s3 cp --recursive hot_backup s3://golddataprotectors/backups/
aws s3 ls s3://golddataprotectors/backups/
```
