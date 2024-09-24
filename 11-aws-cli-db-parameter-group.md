## CLOUD DBA COURSE - DB PARAMETER GROUP


### LIST DB PARAMETER GROUPS
```sh
aws rds describe-db-parameter-groups --profile staging
aws rds describe-db-cluster-parameter-groups --profile staging
aws rds describe-db-parameters --db-parameter-group-name default.mysql8.0 --profile staging
```

### CREATE DB PARAMETER GROUP FOR MYSQL8
```sh
aws rds create-db-parameter-group --db-parameter-group-name "rds-staging-pg" --db-parameter-group-family "mysql8.0" --description "PG for Staging RDS" --profile staging
aws rds describe-db-parameter-groups --profile staging
```


### RESET DB PARAMETER GROUP
```sh
aws rds reset-db-parameter-group --db-parameter-group-name "rds-staging-pg" --reset-all-parameters --profile staging
```


### DELETE DB PARAMETER GROUP
```sh
aws rds delete-db-parameter-group --db-parameter-group-name rds-staging-pg --profile staging
```
