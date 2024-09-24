## CLOUD DBA COURSE - AWS CLI - CREATE ROUTE TABLE


### GET VPC ID
```sh
aws ec2 describe-vpcs --profile staging | jq '.Vpcs[] | {VpcId},{Tags}'
```


### CREATE ROUTE TABLE
```sh
VPC_ID="vpc-00adcb230943229fa"
echo ${VPC_ID}

aws ec2 create-route-table \
    --vpc-id ${VPC_ID} \
    --tag-specifications ResourceType=route-table,Tags='[{Key=Name,Value="staging-RT"}]' \
    --profile staging
```


### GET ROUTE TABLE ID & IGW ID
```sh
aws ec2 describe-route-tables --profile staging | jq '.RouteTables[] | {RouteTableId}, {Tags}'
aws ec2 describe-internet-gateways --profile staging | jq '.InternetGateways[] | {InternetGatewayId}, {Tags}'
```


### CREATE ROUTE
```sh
RT_ID="rtb-08438a620c527f885"
IGW_ID="igw-0f832f33228d0e508"
echo ${RT_ID} ${IGW_ID}

aws ec2 create-route \
    --route-table-id ${RT_ID} \
    --destination-cidr-block "0.0.0.0/0" \
    --gateway-id ${IGW_ID} \
    --profile staging
```


### VERIFY
```sh
aws ec2 describe-route-tables --profile staging | jq '.RouteTables[] | {RouteTableId},{Routes},{Tags}'
```

