## CLOUD DBA COURSE - AWS CLI - ATTACH SUBNETS TO ROUTE TABLE


### GET ROUTE TABLE ID
```sh
aws ec2 describe-route-tables --profile staging | jq '.RouteTables[] | {RouteTableId}, {Tags}'
```

### GET SUBNETS IDS
```sh
aws ec2 describe-subnets --profile staging | jq '.Subnets[] | {CidrBlock},{SubnetId}'
```

### ATTACH SUBNETS TO ROUTE TABLE
```sh
RT_ID="rtb-08438a620c527f885"
SUBNET1_ID="subnet-007b3dfecaf435bff"
SUBNET2_ID="subnet-009f945f39a088ee7"
SUBNET3_ID="subnet-053021207cdb3e960"
echo ${RT_ID} ${SUBNET1_ID} ${SUBNET2_ID} ${SUBNET3_ID}

aws ec2 associate-route-table \
    --subnet-id ${SUBNET1_ID} \
    --route-table-id ${RT_ID} \
    --profile staging

aws ec2 associate-route-table \
    --subnet-id ${SUBNET2_ID} \
    --route-table-id ${RT_ID} \
    --profile staging

aws ec2 associate-route-table \
    --subnet-id ${SUBNET3_ID} \
    --route-table-id ${RT_ID} \
    --profile staging
```



### VERIFY
```sh
aws ec2 describe-route-tables --profile staging | jq '.RouteTables[] | {RouteTableId},{Associations}'
```

