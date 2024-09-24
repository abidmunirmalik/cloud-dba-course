## CLOUD DBA COURSE - AWS CLI - CREATE SUBNET GROUP


### GET SUBNET IDs
```sh
aws ec2 describe-subnets --profile staging | jq '.Subnets[] | {AvailabilityZone}, {CidrBlock},{SubnetId}'
```


### CREATE DB SUBNET GROUP
```sh
aws rds create-db-subnet-group \
    --db-subnet-group-name "rds-staging-subnet-group" \
    --db-subnet-group-description "Subnet Group for RDS Staging" \
    --subnet-ids '["subnet-007b3dfecaf435bff", "subnet-009f945f39a088ee7", "subnet-053021207cdb3e960"]' \
    --profile staging
```


### VERIFY
```sh
aws rds describe-db-subnet-groups --profile staging | jq '.DBSubnetGroups[] | {DBSubnetGroupName},{Subnets}'
```
