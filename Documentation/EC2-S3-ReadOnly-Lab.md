# EC2 to S3 Read-Only IAM Lab

## 1. Objective

The objective of this lab was to implement and validate a secure AWS IAM configuration where an Amazon EC2 instance could access an Amazon S3 bucket using an IAM Role with read-only permissions.

The lab demonstrates:

- IAM Role-based access for EC2
- Least-privilege access to Amazon S3
- IAM policy attachment
- AWS STS identity verification
- S3 bucket and object read access
- Successful S3 object download
- Access-denied behavior for unauthorized operations

---

## 2. Architecture

The lab used the following AWS services:

- Amazon EC2
- Amazon S3
- AWS IAM
- AWS STS
- Amazon VPC
- Security Groups

### Architecture Flow

EC2 Instance
      |
      | IAM Role
      v
EC2-S3-ReadOnly-Role
      |
      | Read-only S3 permissions
      v
Amazon S3 Bucket
geo-iam-s3-lab-2026

The EC2 instance received permissions through an IAM Role instead of storing long-term AWS access keys on the server.

---

## 3. IAM Role

### Role Name

`EC2-S3-ReadOnly-Role`

The IAM Role was attached to the EC2 instance through an EC2 Instance Profile.

This allowed the EC2 instance to obtain temporary AWS credentials automatically.

### Security Principle

The implementation follows the principle of least privilege.

The EC2 instance was given only the permissions required to read objects from S3 rather than full administrative access.

---

## 4. S3 Bucket

### Bucket Name

`geo-iam-s3-lab-2026`

The bucket contained a test object:

`test.txt`

The file was used to validate whether the EC2 instance could read and download objects from S3.

---

## 5. EC2 Configuration

The test EC2 instance was launched using:

- Operating System: Amazon Linux 2023
- Instance Type: t3.micro
- Architecture: 64-bit x86
- Storage: 8 GiB gp3
- IAM Role: `EC2-S3-ReadOnly-Role`
- Security Group: `EC2-S3-Lab-SG`

SSH access was temporarily allowed from the administrator's public IP address.

After the testing was completed, the EC2 instance was terminated to avoid unnecessary AWS charges.

---

## 6. Verify IAM Role Using AWS STS

After connecting to the EC2 instance, the AWS CLI was used to verify the identity associated with the instance.

### Command

```bash
aws sts get-caller-identity
