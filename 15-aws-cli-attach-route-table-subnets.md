## CLOUD DBA COURSE - AWS CLI - ATTACH SUBNETS TO ROUTE TABLE


### GET ROUTE TABLE ID
```sh
aws ec2 describe-route-tables | jq '.RouteTables[] | {RouteTableId}, {Tags}'
```

### GET SUBNETS IDS
```sh
aws ec2 describe-subnets | jq '.Subnets[] | {CidrBlock},{SubnetId}'
```

### ATTACH SUBNETS TO ROUTE TABLE
```sh
RT_ID="rtb-0705daeeef0f7f228"
SUBNET1_ID="subnet-08e4ab9abcb5dd68e"
SUBNET2_ID="subnet-0e78ce016536feaab"
SUBNET3_ID="subnet-0efa7820e3692998d"
echo ${RT_ID} ${SUBNET1_ID} ${SUBNET2_ID} ${SUBNET3_ID}

aws ec2 associate-route-table \
    --subnet-id ${SUBNET1_ID} \
    --route-table-id ${RT_ID}

aws ec2 associate-route-table \
    --subnet-id ${SUBNET2_ID} \
    --route-table-id ${RT_ID}

aws ec2 associate-route-table \
    --subnet-id ${SUBNET3_ID} \
    --route-table-id ${RT_ID}
```



### VERIFY
```sh
aws ec2 describe-route-tables | jq '.RouteTables[] | {RouteTableId},{Associations}'
```

