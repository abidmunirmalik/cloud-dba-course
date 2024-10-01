## CLOUD DATABAE ADMINISTRATION - RDS READ REPLICA


### SECURITY GROUP
```sh
VPC_ID="vpc-052e6de4781367a6c"

aws ec2 create-security-group \
    --vpc-id ${VPC_ID} \
    --group-name "rds-prodreplica-sg" \
    --description "SG for RDS Prod Replica" \
    --tag-specifications ResourceType=security-group,Tags='[{Key=Name,Value="rds-prodreplica-sg"}]' \
    --profile staging
```

### SECURITY GROUP INBOUND RULE
```sh
SEC_ID="sg-02fe45ea84362952e"
echo ${SEC_ID}

aws ec2 authorize-security-group-ingress \
    --group-id ${SEC_ID} \
    --protocol tcp \
    --port 3306 \
    --cidr 0.0.0.0/0 \
    --profile staging
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
  --publicly-accessible \
  --vpc-security-group-ids \
  --storage-type gp3 \
  --no-enable-performance-insights \
  --no-deletion-protection \
  --source-region us-east-1 \
  --region us-east-1 \
  --profile staging
```
