## CLOUD DBA COURSE - DB PARAMETER GROUP


### LIST DB PARAMETER GROUPS
```sh
aws rds describe-db-parameter-groups
aws rds describe-db-cluster-parameter-groups
aws rds describe-db-parameters --db-parameter-group-name default.mysql8.0
```

### CREATE DB PARAMETER GROUP FOR MYSQL8
```sh
aws rds create-db-parameter-group --db-parameter-group-name "demopg" --db-parameter-group-family "mysql8.0" --description "Demo PG"
aws rds describe-db-parameter-groups
```


### RESET DB PARAMETER GROUP
```sh
aws rds reset-db-parameter-group --db-parameter-group-name "demopg" --reset-all-parameters
```


### DELETE DB PARAMETER GROUP
```sh
aws rds delete-db-parameter-group --db-parameter-group-name demopg
```
