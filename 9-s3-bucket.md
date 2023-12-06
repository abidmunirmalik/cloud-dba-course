## CLOUD DBA COURSE -  CREATE S3 BUCKET

### AWS CLI COMMAND TYPES FOR S3
* The AWS CLI provides two tiers of commands for accessing S3 Service.
* **s3** - Used for common tasks like creating, manipulating, and deleting objects
* **s3api** - Exposes direct access to all Amazon S3 API operatings including advanced operations.

  
### USING AWS CLI S3
```sh
aws s3 ls
aws s3 mb s3://golddataprotector
aws s3 ls s3://golddataprotector

echo "A simple file in s3 bucket" > file.txt
aws s3 cp file.txt s3://golddataprotector
aws s3 rm s3://golddataprotector/file.txt
aws s3 rb s3://golddataprotector
```


### USING AWS CLI S3API
```sh
aws s3api list-buckets
aws s3api create-bucket --bucket golddataprotector --region us-east-1
aws s3api put-object --bucket golddataprotector --key backups/
aws s3api put-object --bucket golddataprotector --key backups/full_backup/world/countries.ibd
aws s3api delete-bucket --bucket golddataprotector
aws s3api list-objects --bucket golddataprotector --query "Contents[].{Key: Key}" --output text | while read -r line; do aws s3api delete-object --bucket golddataprotector --key "$line"; done
aws s3api get-bucket-policy --bucket my-bucket
aws s3api get-bucket-acl --bucket my-bucket

aws s3api create-bucket --bucket golddataprotectors --region us-east-1
aws s3api put-object --bucket golddataprotectors --key backups/full_backup
```
