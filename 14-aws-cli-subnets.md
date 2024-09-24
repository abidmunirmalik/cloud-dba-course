## CLOUD DBA COURSE - AWS CLI - CREATE SUBNETS


### GET VPC ID
```sh
aws ec2 describe-vpcs | jq '.Vpcs[] | {VpcId},{Tags}'
```


### CREATE SUBNETS
```sh
VPC_ID="vpc-00adcb230943229fa"
SUBNET1_CIDR="10.10.1.0/24"
SUBNET2_CIDR="10.10.2.0/24"
SUBNET3_CIDR="10.10.3.0/24"
echo ${VPC_ID} ${SUBNET1_CIDR} ${SUBNET2_CIDR} ${SUBNET3_CIDR}

aws ec2 create-subnet \
    --vpc-id ${VPC_ID} \
    --cidr-block ${SUBNET1_CIDR} \
    --availability-zone "us-east-1a" \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="public-staging-1a"}]' \
    --profile staging

aws ec2 create-subnet \
    --vpc-id ${VPC_ID} \
    --cidr-block ${SUBNET2_CIDR} \
    --availability-zone "us-east-1b" \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="public-staging-1b"}]' \
    --profile staging

aws ec2 create-subnet \
    --vpc-id ${VPC_ID} \
    --cidr-block ${SUBNET3_CIDR} \
    --availability-zone "us-east-1c" \
    --tag-specifications ResourceType=subnet,Tags='[{Key=Name,Value="public-staging-1c"}]' \
    --profile staging
```



### VERIFY
```sh
aws ec2 describe-subnets | jq '.Subnets[] | {AvailabilityZone}, {CidrBlock},{SubnetId}'
```

