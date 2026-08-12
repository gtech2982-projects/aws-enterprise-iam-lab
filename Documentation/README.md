# AWS Enterprise IAM Lab — Documentation

This directory contains the detailed documentation for the AWS Enterprise IAM Lab.

The project demonstrates practical AWS Identity and Access Management (IAM), including IAM users, groups, custom policies, IAM roles, least-privilege access, and secure EC2-to-S3 communication using temporary credentials.

## 📚 Documentation

### 1. Business Requirements

[View Business Requirements](Business-Requirement.md)

Describes the business scenario, access requirements, IAM user/group structure, and security objectives used to design the environment.

### 2. EC2-to-S3 Read-Only Lab

[View EC2-to-S3 Read-Only Lab](EC2-S3-ReadOnly-Lab.md)

Documents the practical implementation of secure EC2-to-S3 access using an IAM role.

The lab includes:

- Creating an IAM role for EC2
- Attaching an S3 read-only policy
- Launching an Amazon EC2 instance
- Attaching the IAM role to EC2
- Connecting to the Linux instance
- Verifying the assumed role using AWS STS
- Listing S3 buckets and objects using AWS CLI
- Downloading `test.txt`
- Testing an unauthorized operation
- Confirming `AccessDenied`
- Cleaning up temporary AWS resources

## 🔐 Security Concepts Demonstrated

- Principle of Least Privilege
- Role-Based Access Control
- IAM Users and Groups
- IAM Policies
- IAM Roles
- Temporary AWS Credentials
- AWS STS
- EC2 Instance Profiles
- S3 Access Control
- Allowed vs. Denied Permission Testing
- Avoiding Hard-Coded AWS Credentials

## 🏗️ Architecture

The EC2-to-S3 access flow implemented in the project is:

`EC2 Instance → IAM Role → AWS STS Temporary Credentials → Amazon S3`

The full architecture diagram is available in the repository's `Architecture` directory.

## 🎯 Project Objective

The objective of this project is to demonstrate practical AWS IAM administration and cloud security concepts through a hands-on environment rather than theoretical configuration alone.
