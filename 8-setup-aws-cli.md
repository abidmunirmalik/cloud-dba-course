## CLOUD DBA COURSE -  SETUP AWS CLI


### FRESH INSTALL - AWS CLI Version 2
```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```


### UPDATE FROM AWS CLI TO AWS CLI Version 2
```sh
rpm -qa | grep awscli
aws --version
sudo yum remove awscli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws configure
```


### CONFIGURE AWS
```sh
aws configure
AWS Access Key ID [None]: AWS-ACCESS-KEY
AWS Secret Access Key [None]: AWS-SECRET-ACCESS-KEY
Default region name [None]: us-east-1
Default output format [None]: json

aws configure list
aws configure list-profiles

aws sts get-caller-identity
aws ec2 describe-instances
```
