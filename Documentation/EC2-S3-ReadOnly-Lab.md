# EC2 to S3 Read-Only IAM Lab

## Objective

This practical lab demonstrates how to securely grant an Amazon EC2 instance read-only access to an Amazon S3 bucket using an IAM role.

The implementation follows the principle of least privilege by allowing the EC2 instance to read objects from S3 while preventing upload and deletion operations.

---

## Architecture

EC2 Instance
↓
IAM Role
`EC2-S3-ReadOnly-Role`
↓
IAM Policy
`CloudEngineers-S3-ReadOnly`
↓
Amazon S3 Bucket
`geo-iam-s3-lab-2026`

---

## AWS Services Used

- Amazon EC2
- Amazon S3
- AWS IAM
- IAM Roles
- IAM Policies
- AWS CLI
- EC2 Instance Connect

---

## Implementation

### 1. IAM Role

Created an IAM role:

`EC2-S3-ReadOnly-Role`

The role allows an EC2 instance to make AWS API calls using temporary credentials.

### 2. IAM Policy

Attached the following customer-managed policy:

`CloudEngineers-S3-ReadOnly`

The policy provides read-only S3 permissions.

### 3. EC2 Instance

Created an Amazon Linux 2023 EC2 instance:

- Instance type: `t3.micro`
- IAM Role: `EC2-S3-ReadOnly-Role`
- IMDSv2: Required
- Security Group: `EC2-S3-Lab-SG`

### 4. S3 Bucket

Created the S3 bucket:

`geo-iam-s3-lab-2026`

Uploaded a test object:

`test.txt`

---

## Permission Testing

Connected to the EC2 instance using EC2 Instance Connect.

### Verify AWS CLI

```bash
aws --version
