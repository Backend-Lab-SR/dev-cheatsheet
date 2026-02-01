# AWS CLI Cheatsheet

## Configuration

```bash
aws configure
aws configure --profile <profile-name>
aws configure list-profiles
aws configure set region us-east-1
aws configure set output json
aws configure list

aws <command> --profile <profile-name>
aws <command> --region us-west-2
aws <command> --output json
aws <command> --output table
aws <command> --dry-run
```

## EC2

```bash
aws ec2 describe-instances
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
aws ec2 start-instances --instance-ids <instance-id>
aws ec2 stop-instances --instance-ids <instance-id>
# WARNING: Destructive
aws ec2 terminate-instances --instance-ids <instance-id>
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name <key-name>
aws ec2 describe-images --owners self
aws ec2 describe-security-groups
aws ec2 describe-key-pairs
```

## S3

```bash
aws s3 ls
aws s3 ls s3://bucket-name
aws s3 mb s3://bucket-name --region us-east-1
# WARNING: Destructive
aws s3 rb s3://bucket-name --force
aws s3 cp file.txt s3://bucket-name/
aws s3 cp s3://bucket-name/file.txt ./
aws s3 cp ./local-folder s3://bucket-name/ --recursive
aws s3 sync ./local-folder s3://bucket-name/folder/
aws s3 sync s3://bucket-name/folder/ ./local-folder
aws s3 rm s3://bucket-name/file.txt
aws s3 rm s3://bucket-name/folder/ --recursive
aws s3 presign s3://bucket-name/file.txt --expires-in 3600
```

## IAM

```bash
aws iam list-users
aws iam list-roles
aws iam list-policies
aws iam get-user --user-name <username>
aws iam create-user --user-name <username>
aws iam create-access-key --user-name <username>
aws iam list-access-keys --user-name <username>
aws iam attach-user-policy --user-name <username> --policy-arn <policy-arn>
aws sts get-caller-identity
```

## Lambda

```bash
aws lambda list-functions
aws lambda get-function --function-name <function-name>
aws lambda invoke --function-name <function-name> output.json
aws lambda update-function-code --function-name <function-name> --zip-file fileb://function.zip
aws lambda list-versions-by-function --function-name <function-name>
# WARNING: Destructive
aws lambda delete-function --function-name <function-name>
```

## CloudFormation

```bash
aws cloudformation create-stack --stack-name <stack-name> --template-body file://template.yaml
aws cloudformation update-stack --stack-name <stack-name> --template-body file://template.yaml
aws cloudformation describe-stacks --stack-name <stack-name>
aws cloudformation list-stacks
# WARNING: Destructive
aws cloudformation delete-stack --stack-name <stack-name>
aws cloudformation describe-stack-events --stack-name <stack-name>
```

## ECS

```bash
aws ecs list-clusters
aws ecs list-services --cluster <cluster-name>
aws ecs list-tasks --cluster <cluster-name>
aws ecs list-tasks --cluster <cluster-name> --service-name <service-name>
aws ecs describe-tasks --cluster <cluster-name> --tasks <task-arn>
aws ecs run-task --cluster <cluster-name> --task-definition <task-def>
aws ecs stop-task --cluster <cluster-name> --task <task-arn>
aws ecs update-service --cluster <cluster-name> --service <service-name> --desired-count 3
```

## ECR

```bash
aws ecr describe-repositories
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
aws ecr list-images --repository-name <repo-name>
aws ecr batch-delete-image --repository-name <repo-name> --image-ids imageTag=<tag>
```

## CloudWatch & Logs

```bash
aws logs describe-log-groups
aws logs get-log-events --log-group-name <log-group> --log-stream-name <log-stream>
aws logs tail <log-group-name> --follow
aws cloudwatch list-metrics --namespace AWS/EC2
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization --dimensions Name=InstanceId,Value=<instance-id> --start-time 2023-01-01T00:00:00Z --end-time 2023-01-02T00:00:00Z --period 3600 --statistics Average
```

## RDS

```bash
aws rds describe-db-instances
aws rds create-db-instance --db-instance-identifier <id> --db-instance-class db.t2.micro --engine mysql --master-username admin --master-user-password <password> --allocated-storage 20
# WARNING: Destructive
aws rds delete-db-instance --db-instance-identifier <id> --skip-final-snapshot
aws rds create-db-snapshot --db-instance-identifier <id> --db-snapshot-identifier <snapshot-id>
```

## Utilities

```bash
aws <service> help
aws help | grep -A 100 "AVAILABLE SERVICES"
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name]' --output table
```

```bash
alias aws-whoami='aws sts get-caller-identity'
alias aws-regions='aws ec2 describe-regions --query "Regions[].{Name:RegionName}" --output text'
alias aws-account='aws sts get-caller-identity --query Account --output text'
```
