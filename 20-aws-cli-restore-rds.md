## CLOUD DBA COURSE - AWS CLI - RESTORE RDS FROM HOT BACKUP IN S3 BUCKET 


### CREATE RDS INSTANCE
```sh
aws rds restore-db-instance-from-s3 \
  --region us-east-1 \
  --db-instance-identifier staging \
  --allocated-storage 50 \
  --max-allocated-storage 200 \
  --storage-encrypted \
  --storage-type gp3 \
  --db-instance-class db.t3.small \
  --engine mysql  \
  --master-username master \
  --master-user-password stagingTmkMbdNHLtC2U \
  --s3-bucket-name "golddataprotectors" \
  --s3-prefix "backups/" \
  --s3-ingestion-role-arn "arn:aws:iam::004555066016:role/RDSToS3BucketAccess" \
  --source-engine mysql \
  --source-engine-version 8.0.35 \
  --vpc-security-group-ids "sg-0a990980f4ae0da90" \
  --db-subnet-group-name "rds-staging-subnet-group" \
  --db-parameter-group-name "rds-staging-pg" \
  --enable-performance-insights \
  --performance-insights-retention-period 7 \
  --no-deletion-protection \
  --no-auto-minor-version-upgrade \
  --profile staging
```


### VERIFY
```sh
aws rds describe-db-instances --profile staging | jq '.DBInstances[] | {DBInstanceIdentifier},{DBInstanceClass},{Endpoint}'
```
