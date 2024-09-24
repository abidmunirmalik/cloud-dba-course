## CLOUD DBA COURSE - AWS CLI - CREATE VPC, IGW


### CREATE VPC
```sh
VPC_CIDR=10.10.0.0/16
aws ec2 create-vpc \
    --no-amazon-provided-ipv6-cidr-block \
    --cidr-block ${VPC_CIDR} \
    --instance-tenancy default \
    --region us-east-1 \
    --tag-specifications ResourceType=vpc,Tags='[{Key=Name,Value="staging-vpc"}]'
```


### CREATE INTERNET GATEWAY IGW
```sh
aws ec2 create-internet-gateway \
    --tag-specifications ResourceType=internet-gateway,Tags='[{Key=Name,Value="staging-IGW"}]'
```


### QUERY VPC & IGW INFORMATION
```sh
aws ec2 describe-vpcs
aws ec2 describe-vpcs | jq '.Vpcs[] | {VpcId},{Tags}'
aws ec2 describe-internet-gateways | jq '.InternetGateways[] | {InternetGatewayId},{Tags}'
```


### ATTACH IGW TO VPC
```sh
VPC_ID="vpc-083591f5a14845d54"
IGW_ID="igw-0565accf018557bb1"
echo ${VPC_ID} ${IGW_ID}

aws ec2 attach-internet-gateway \
    --internet-gateway-id ${IGW_ID} \
    --vpc-id ${VPC_ID}
```


### VERIFY
```sh
aws ec2 describe-internet-gateways | jq '.InternetGateways[] | {InternetGatewayId},{Attachments}'
```

