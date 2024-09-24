## CLOUD DBA COURSE - AWS CLI - CREATE SUBNET GROUP


### GET SUBNET IDs
```sh
aws ec2 describe-subnets | jq '.Subnets[] | {AvailabilityZone}, {CidrBlock},{SubnetId}'
```


### CREATE DB SUBNET GROUP
```sh
SUBNET1_ID="subnet-08e4ab9abcb5dd68e"
SUBNET2_ID="subnet-0e78ce016536feaab"
SUBNET3_ID="subnet-0efa7820e3692998d"
echo ${SUBNET1_ID} ${SUBNET2_ID} ${SUBNET3_ID}

aws rds create-db-subnet-group \
    --db-subnet-group-name "rds-staging-subnet-group" \
    --db-subnet-group-description "Subnet Group for RDS Staging" \
    --subnet-ids '["subnet-08e4ab9abcb5dd68e", "subnet-0e78ce016536feaab", "subnet-0efa7820e3692998d"]'
```


### VERIFY
```sh
aws rds describe-db-subnet-groups | jq '.DBSubnetGroups[] | {DBSubnetGroupName},{Subnets}'
```
