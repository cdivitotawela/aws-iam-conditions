
## Assume Role with External Id
Account `A` has role `auditor` which can be assumed by the account `B`
user `auditor` allows to list the buckets. Setup the IAM user `auditor` in account `B` with 
AWS CLI configuration to assume the `auditor` role and list bucket. Role `auditor` can be assumed
with the external id `2231`.


1. Create role `auditor` in account `A` using the cloudformation template [cfn-account-a-role.yaml](cfn-account-a-role.yaml)
2. Create `auditor` IAM user in the account `B` using the the cloudformation teamplate [cfn-account-b-user.yaml](cfn-account-b-user.yaml)
3. Create access key for the IAM user and note down the access key id and secret key 
4. Configure the AWS CLI
```shell
# Run the command and configure the IAM access key id and secret key
export AWS_PROFILE=user 
aws configure
```
5. Configure the AWS profile `auditor` to assume the role
```shell
[profile auditor]
role_arn = arn:aws:iam::<account id of account A>:role/Auditor
source_profile = user
external_id = 2231
```

6. List buckets assuming the role
```shell
export AWS_PROFILE=auditor
aws s3 ls
```


