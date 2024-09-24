## CLOUD DBA COURSE - AWS CLI - CREATE ROUTE TABLE


### GET VPC ID
```sh
aws ec2 describe-vpcs | jq '.Vpcs[] | {VpcId},{Tags}'
```


### CREATE ROUTE TABLE
```sh
VPC_ID="vpc-083591f5a14845d54"
echo ${VPC_ID}

aws ec2 create-route-table \
    --vpc-id ${VPC_ID} \
    --tag-specifications ResourceType=route-table,Tags='[{Key=Name,Value="staging-RT"}]'
```


### GET ROUTE TABLE ID & IGW ID
```sh
aws ec2 describe-route-tables | jq '.RouteTables[] | {RouteTableId}, {Tags}'
aws ec2 describe-internet-gateways | jq '.InternetGateways[] | {InternetGatewayId}, {Tags}'
```


### CREATE ROUTE
```sh
RT_ID="rtb-0705daeeef0f7f228"
IGW_ID="igw-0565accf018557bb1"
echo ${RT_ID} ${IGW_ID}

aws ec2 create-route \
    --route-table-id ${RT_ID} \
    --destination-cidr-block "0.0.0.0/0" \
    --gateway-id ${IGW_ID}
```


### VERIFY
```sh
aws ec2 describe-route-tables | jq '.RouteTables[] | {RouteTableId},{Routes},{Tags}'
```

