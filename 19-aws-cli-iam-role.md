## CLOUD DBA COURSE - AWS CLI - CREATE IAM ROLE FOR RDS

### CREATE TRUST POLICY JSON DOCUMENT
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "",
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "rds.amazonaws.com"
                ]
            },
            "Action": [
                "sts:AssumeRole"
            ]
        }
    ]
}
```


### CREATE IAM ROLE
```sh
aws iam create-role --role-name "RDSToS3BucketAccess" --assume-role-policy-document file://trust_policy.json
```


### GET POLICY ARN
```sh
aws iam list-policies | jq '.Policies[] | {PolicyName},{Arn}' | grep -i "AmazonS3FullAccess"
```


### ATTACH POLICY TO IAM ROLE
```sh
aws iam attach-role-policy \
    --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess \
    --role-name RDSToS3BucketAccess
```


### VERIFY
```sh
aws iam list-roles | jq '.Roles[] | {RoleName}'
```
