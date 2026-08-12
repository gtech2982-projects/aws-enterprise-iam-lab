# IAM Policies

This directory contains the custom AWS IAM policies used in the AWS Enterprise IAM Lab.

The policies were created to demonstrate role-based access control and the principle of least privilege.

## Policies Included

### 1. Developers-EC2-Policy.json

Provides limited EC2 access for members of the `Developers` group.

Allowed actions include:

- `ec2:DescribeInstances`
- `ec2:DescribeVolumes`
- `ec2:DescribeInstanceStatus`
- `ec2:DescribeSnapshots`
- `ec2:StartInstances`
- `ec2:StopInstances`

The policy allows developers to view and operate existing EC2 instances without granting full EC2 administrative permissions.

### 2. CloudEngineers-S3-ReadOnly.json

Provides read-only Amazon S3 access for members of the `CloudEngineers` group and for the EC2 IAM role used in the S3 access lab.

Allowed actions include:

- `s3:ListAllMyBuckets`
- `s3:GetBucketLocation`
- `s3:ListBucket`
- `s3:GetObject`

The policy intentionally does not include:

- `s3:PutObject`
- `s3:DeleteObject`

This was validated during testing:

- S3 bucket listing: Allowed
- Object listing: Allowed
- Object download: Allowed
- Upload: Denied
- Delete: Denied

## Security Principle

Both policies are designed around the principle of least privilege.

Only the permissions required for the intended task are granted, while unnecessary write or administrative actions remain restricted.

## Policy Files

- [Developers EC2 Policy](Developers-EC2-Policy.json)
- [Cloud Engineers S3 Read-Only Policy](CloudEngineers-S3-ReadOnly.json)
