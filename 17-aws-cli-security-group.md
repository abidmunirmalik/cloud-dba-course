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
    --group-name "rds-staging-sg" \
    --description "SG for RDS Dev" \
    --tag-specifications ResourceType=security-group,Tags='[{Key=Name,Value="rds-staging-sg"}]'
```

### GET SECURITY ID
```sh
aws ec2 describe-security-groups | jq '.SecurityGroups[] | {VpcId},{GroupId},{Tags}'
```


### CREATE INBOUND RULE
```sh
SEC_ID="sg-0d40d9597e090c615"
echo ${SEC_ID}

aws ec2 authorize-security-group-ingress \
    --group-id ${SEC_ID} \
    --protocol tcp \
    --port 3306 \
    --cidr 0.0.0.0/0 
```


### VERIFY
```sh
aws ec2 describe-security-groups | jq '.SecurityGroups[] | {VpcId},{GroupId},{Tags}'
```
