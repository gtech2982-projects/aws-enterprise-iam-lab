# AWS Enterprise IAM Lab

A hands-on AWS Identity and Access Management (IAM) project demonstrating secure user access, group-based permissions, IAM roles, least-privilege policies, and EC2-to-S3 access using temporary credentials.

## 📌 Project Overview

This project simulates an enterprise-style AWS IAM environment where access to AWS resources is controlled through users, groups, policies, and roles.

The project demonstrates how AWS IAM can be used to:

- Create and manage IAM users and groups
- Assign permissions based on job responsibilities
- Implement least-privilege access
- Configure custom IAM policies
- Use IAM roles with Amazon EC2
- Provide secure EC2-to-S3 access without hard-coded credentials
- Verify role identity using AWS STS
- Test allowed and denied AWS operations
- Apply basic AWS security best practices

---

## 🏗️ Architecture

The project uses AWS IAM as the central access-control layer.

```text
IAM Users
    │
    ├── Developers
    │      └── EC2 Permissions
    │
    └── CloudEngineers
           └── S3 Read Permissions


EC2 Instance
    │
    │ IAM Role
    ▼
EC2-S3-ReadOnly-Role
    │
    │ Temporary AWS Credentials
    ▼
Amazon S3
    │
    ▼
geo-iam-s3-lab-2026
    │
    └── test.txt
```

---

## ☁️ AWS Services Used

| AWS Service | Purpose |
|---|---|
| AWS IAM | Identity and access management |
| Amazon EC2 | Compute instance used for role testing |
| Amazon S3 | Storage used for permission testing |
| AWS STS | Verification of assumed IAM role |
| Amazon VPC | Network environment for EC2 |
| Security Groups | Control inbound network access |
| AWS CLI | Test AWS permissions from EC2 |

---

## 🔐 IAM Components

### IAM Users

IAM users were created to simulate individual users within an organization.

Example users included:

- `alice.dev`
- `Charlie.cloud`

### IAM Groups

Users were organized into groups based on their responsibilities.

Examples:

- `Developers`
- `CloudEngineers`

Permissions were assigned through IAM policies instead of granting unnecessary administrative access.

---

## 📜 Custom IAM Policies

Custom policies were created to control access to AWS resources.

Examples include:

```text
Developers-EC2-Policy
CloudEngineers-S3-ReadOnly
```

The S3 read-only policy allowed required read operations while preventing unauthorized write operations.

This demonstrates the AWS security principle of:

> **Least Privilege — grant only the permissions required to perform a task.**

---

## 🖥️ EC2 → S3 IAM Role Lab

A dedicated IAM role was created:

```text
EC2-S3-ReadOnly-Role
```

The role was attached to an Amazon EC2 instance.

Instead of configuring permanent AWS access keys on the instance, EC2 obtained temporary credentials through its IAM role.

The role was then tested from the EC2 Linux environment using the AWS CLI.

---

## 🔎 IAM Role Verification

The identity being used by the EC2 instance was verified using:

```bash
aws sts get-caller-identity
```

The returned ARN showed:

```text
assumed-role/EC2-S3-ReadOnly-Role
```

This confirmed that the EC2 instance was successfully operating through the IAM role.

---

## 🪣 S3 Permission Testing

The EC2 instance successfully listed the available S3 bucket:

```bash
aws s3 ls
```

The lab bucket was visible:

```text
geo-iam-s3-lab-2026
```

The objects inside the bucket were then listed:

```bash
aws s3 ls s3://geo-iam-s3-lab-2026/
```

The test object was successfully identified:

```text
test.txt
```

---

## 📥 S3 Object Download

The EC2 instance successfully downloaded the test object:

```bash
aws s3 cp s3://geo-iam-s3-lab-2026/test.txt .
```

The downloaded file was verified using:

```bash
cat test.txt
```

This demonstrated successful S3 read access through the EC2 IAM role.

---

## 🚫 Unauthorized Access Test

An operation outside the permitted read-only access was tested.

AWS returned:

```text
AccessDenied
```

This was the expected result.

The test demonstrated that the IAM policy allowed required read operations while preventing unauthorized actions.

---

## ✅ Security Controls Demonstrated

| Control | Result |
|---|---|
| IAM users and groups | ✅ Implemented |
| Custom IAM policies | ✅ Implemented |
| Least-privilege permissions | ✅ Implemented |
| EC2 IAM role | ✅ Implemented |
| Temporary role credentials | ✅ Verified |
| AWS STS identity verification | ✅ Passed |
| S3 bucket listing | ✅ Passed |
| S3 object listing | ✅ Passed |
| S3 object download | ✅ Passed |
| Unauthorized operation | ✅ Access Denied |
| Hard-coded credentials on EC2 | ❌ Not used |

---

## 📂 Repository Structure

```text
aws-enterprise-iam-lab/
│
├── Architecture/
│
├── Documentation/
│   ├── Business-Requirement.md
│   └── EC2-S3-ReadOnly-Lab.md
│
├── Policies/
│   ├── Developers-EC2-Policy.json
│   └── CloudEngineers-S3-ReadOnly.json
│
├── Screenshots/
│   ├── 01-IAM-User-Groups.png
│   ├── 02-IAM-Users.png
│   └── 03-Alice-Console-Access.png
│
├── .gitignore
└── README.md
```

---

## 🧪 Key Commands Used

```bash
aws --version

aws sts get-caller-identity

aws s3 ls

aws s3 ls s3://geo-iam-s3-lab-2026/

aws s3 cp s3://geo-iam-s3-lab-2026/test.txt .

cat test.txt
```

---

## 🎯 Key Skills Demonstrated

- AWS Identity and Access Management (IAM)
- IAM Users and Groups
- IAM Roles
- IAM Policies
- Principle of Least Privilege
- Amazon EC2
- Amazon S3
- AWS STS
- AWS CLI
- Linux
- Security Groups
- Access-control troubleshooting
- Cloud security fundamentals

---

## 📚 Detailed Documentation

Detailed implementation and testing information is available in:

`Documentation/EC2-S3-ReadOnly-Lab.md`

---

## 🧹 Resource Cleanup

After completing the EC2-to-S3 testing, the temporary EC2 instance was terminated to avoid unnecessary AWS resource usage and charges.

---

## 🏆 Project Outcome

This project demonstrates practical implementation of AWS identity and access management rather than only theoretical IAM knowledge.

The environment successfully demonstrated:

**IAM User → IAM Group → IAM Policy**

and

**EC2 → IAM Role → AWS STS → Amazon S3**

The project validates both **successful authorized access** and **blocked unauthorized access**, demonstrating practical application of least-privilege security in AWS.
## 🏆 Project Outcome

This project demonstrates practical implementation of AWS identity and access management rather than only theoretical IAM knowledge.

The environment successfully demonstrated:

**IAM User → IAM Group → IAM Policy**

and

**EC2 → IAM Role → AWS STS → Amazon S3**

The project validates both **successful authorized access** and **blocked unauthorized access**, demonstrating practical application of least-privilege security in AWS.

---

## 📚 Project Resources

- [Architecture Diagram](Architecture/aws-iam-architecture.png)
- [Architecture Documentation](Architecture/README.md)
- [Business Requirements](Documentation/Business-Requirement.md)
- [EC2-to-S3 Read-Only Lab](Documentation/EC2-S3-ReadOnly-Lab.md)
- [IAM Policies](Policies/README.md)
- [Project Screenshots](Screenshots/README.md)
