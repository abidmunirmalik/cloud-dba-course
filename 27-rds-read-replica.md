## CLOUD DATABAE ADMINISTRATION - RDS READ REPLICA


### SECURITY GROUP
```sh
VPC_ID=""

aws ec2 create-security-group \
    --vpc-id ${VPC_ID} \
    --group-name "rds-prodreplica-sg" \
    --description "SG for RDS Prod Replica" \
    --tag-specifications ResourceType=security-group,Tags='[{Key=Name,Value="rds-prodreplica-sg"}]' \
    --profile staging
```

### PARAMETER GROUP
```sh
aws rds create-db-parameter-group \
  --db-parameter-group-name "rds-prodreplica-pg" \
  --db-parameter-group-family "mysql8.0" \
  --description "PG for RDS Replica" \
  --profile staging
```

### SUBNET GROUP
```sh
```

### RDS READ REPLICA
```sh
aws rds create-db-instance-read-replica \
  --db-instance-identifier prod-replica \
  --source-db-instance-identifier prod \
  --db-instance-class db.t3.small \
  --availability-zone us-east-1b \
  --no-multi-az \
  --no-auto-minor-version-upgrade \
  --db-parameter-group-name rds-prodreplica-pg \
  --publicly-accessible \
  --db-subnet-group-name rds-sg \
  --vpc-security-group-ids \
  --storage-type gp3 \
  --no-enable-performance-insights \
  --no-deletion-protection \
  --source-region us-east-1 \
  --region us-east-1 \
  --profile staging
```
