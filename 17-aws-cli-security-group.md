## CLOUD DBA COURSE - AWS CLI - CREATE SECURITY GROUP


### GET VPC ID
```sh
aws ec2 describe-vpcs | jq '.Vpcs[] | {VpcId},{Tags}'
```


### CREATE SECURITY GROUP
```sh
VPC_ID="vpc-083591f5a14845d54"
echo ${VPC_ID}

aws ec2 create-security-group \
    --vpc-id ${VPC_ID} \
    --group-name "dev-rds-sg" \
    --description "SG for RDS Dev" \
    --tag-specifications ResourceType=security-group,Tags='[{Key=Name,Value="dev-rds-sg"}]'
```

### VERIFY
```sh
aws ec2 describe-security-groups | jq '.SecurityGroups[] | {VpcId},{GroupId},{Tags}'
```
