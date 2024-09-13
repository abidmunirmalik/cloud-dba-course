## CLOUD DBA COURSE - AWS EC2 Specifications

### VPC SETUP
```sh
Name:     prod
CIDR:     192.168.0.0/16
Subnet 1: 192.168.1.0/24
Subnet 2: 192.168.2.0/24
Subnet 3: 192.168.3.0/24

Attach IGW to VPC
```

### SECURITY GROUP SETUP
```sh
Name: mysql-sg
Inbound Rules:
  MySQL/Aurora - 3306 - Internet
  SSH - 22 - Internet
Outbound Rules:
  All - All - 0.0.0.0/0
```

### EC2 INSTANCE
```sh
Name: cloud-replica
Security Group: mysql-sg
AMI-ID: Red Hat Enterprise Linux version 9 (HVM), EBS General Purpose (SSD) Volume Type - ami-0583d8c7a9c35822c
Key-Pair:
  Name: ec2-cloud-db
  Key pair type: ED25519
  Private key file format: .pem
Subnet: No Preference (prod vpc)
Public IP: YES
Block Device: 10 GB gp3
Instance Type: t2.small
```
