# AWS Enterprise IAM Lab — Business Requirements

## 1. Project Background

An organization requires a secure AWS Identity and Access Management (IAM) environment for employees with different job responsibilities.

The objective is to provide users and AWS workloads with only the permissions required to perform their assigned tasks.

The environment should follow the AWS security principle of least privilege and avoid unnecessary administrative access.

---

## 2. Business Requirements

The organization requires:

- Individual IAM identities for users.
- Users to be organized into groups based on job responsibilities.
- Permissions to be assigned through IAM policies.
- Developers to receive permissions required for EC2-related activities.
- Cloud engineers to receive read-only access to Amazon S3.
- AWS workloads to use IAM roles instead of hard-coded AWS access keys.
- Unauthorized operations to be denied.
- Access permissions to be tested and verified.

---

## 3. IAM User Requirements

The lab uses the following example IAM users:

| IAM User | Role / Responsibility |
|---|---|
| `alice.dev` | Developer |
| `Charlie.cloud` | Cloud Engineer |

Users should receive permissions primarily through IAM groups rather than individual permission assignments.

---

## 4. IAM Group Requirements

### Developers

The `Developers` group provides permissions required for EC2-related activities.

Associated policy:

`Developers-EC2-Policy`

### CloudEngineers

The `CloudEngineers` group provides read access to Amazon S3.

Associated policy:

`CloudEngineers-S3-ReadOnly`

This separation demonstrates role-based permission management.

---

## 5. Least-Privilege Requirement

Permissions should follow the principle of least privilege.

Users and workloads should receive only the permissions necessary to perform their required tasks.

For example, S3 read access should permit required operations while unauthorized write operations remain blocked.

---

## 6. EC2 Workload Requirement

An Amazon EC2 instance must access Amazon S3 without storing permanent AWS access keys on the instance.

To accomplish this, the EC2 instance uses:

`EC2-S3-ReadOnly-Role`

The IAM role provides temporary AWS credentials to the EC2 workload.

---

## 7. S3 Access Requirement

The EC2 instance must be able to access the lab S3 bucket:

`geo-iam-s3-lab-2026`

Required operations include:

- List S3 buckets
- List objects in the lab bucket
- Download `test.txt`
- Read the downloaded test file

Unauthorized write operations should return:

`AccessDenied`

---

## 8. IAM Role Verification Requirement

The EC2 instance's AWS identity must be verified using AWS STS.

Verification command:

```bash
aws sts get-caller-identity
