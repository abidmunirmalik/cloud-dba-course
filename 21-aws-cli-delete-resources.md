## CLOUD DBA COURSE - AWS CLI DELETE RESOURCES

### DELETE RDS INSTANCE
```sh
aws rds delete-db-instance --db-instance-identifier staging --region us-east-1 --skip-final-snapshot --profile staging
```


### DELETE PARAMETER GROUP
```sh
aws rds delete-db-parameter-group --db-parameter-group-name rds-staging-pg --profile staging
```

### DELETE DB SUBNET GROUP
```sh
aws rds delete-db-subnet-group --db-subnet-group-name rds-staging-subnet-group --profile staging
```

### DELETE S3 BUCKET
```sh
aws s3 rb s3://golddataprotectors --profile staging
```

### DELETE VPC SECURITY GROUP
```sh
aws ec2 delete-security-group --group-id sg-0a990980f4ae0da90 --profile staging
```

### DELETE SUBNETS
```sh
aws ec2 delete-subnet --subnet-id subnet-007b3dfecaf435bff --profile staging
aws ec2 delete-subnet --subnet-id subnet-009f945f39a088ee7 --profile staging
aws ec2 delete-subnet --subnet-id subnet-053021207cdb3e960 --profile staging
```

### DELETE ROUTE TABLE
```sh
aws ec2 delete-route-table --route-table-id rtb-08438a620c527f885 --profile staging
```

### DETACH IGW AND DELETE
```sh
aws ec2 detach-internet-gateway --internet-gateway-id igw-0f832f33228d0e508 --vpc-id vpc-00adcb230943229fa --profile staging
aws ec2 delete-internet-gateway --internet-gateway-id igw-0f832f33228d0e508 --profile staging
```

### DELETE VPC
```sh
aws ec2 delete-vpc --vpc-id vpc-00adcb230943229fa --profile staging
```
