# AWS S3 and Storage Services – Hands-On Notes

This document serves as a comprehensive reference for Amazon S3 and other AWS storage services. It includes detailed definitions, practical examples, CLI usage, and best practices based on hands-on labs and learning.

---

## 🔹 Types of AWS Storage Solutions

### 1. Amazon S3 (Simple Storage Service)

Amazon S3 is an **object storage service** designed for durability, scalability, and security. It stores unstructured data as **objects** in **buckets**, making it suitable for storing backups, logs, static files, images, videos, and large datasets.

Key features:
- 99.999999999% durability
- Unlimited storage
- Object versioning
- Lifecycle management
- Server-side encryption
- Access control with IAM and bucket policies

---

## 🔹 Amazon S3 Storage Classes and Use Cases

Amazon S3 offers multiple storage classes optimized for different use cases:

### 1. S3 Standard

- **Description**: Default storage class for frequently accessed data.
- **Use Case**: Dynamic websites, data analytics, active content.
- **Durability**: 99.999999999%
- **Availability**: High (across multiple AZs)
- **Cost**: Highest among S3 tiers, but optimized for frequent access.

### 2. S3 Intelligent-Tiering

- **Description**: Automatically moves data between frequent and infrequent access tiers based on usage.
- **Use Case**: Unknown or unpredictable access patterns.
- **Durability**: 99.999999999%
- **Availability**: High
- **Cost**: Slightly higher than Standard for small objects due to monitoring overhead but saves money on infrequently accessed data.

### 3. S3 Standard-Infrequent Access (Standard-IA)

- **Description**: Lower-cost storage for data accessed less frequently.
- **Use Case**: Backups, long-lived but infrequently accessed content.
- **Durability**: 99.999999999%
- **Availability**: 99.9%
- **Cost**: Lower storage costs with a retrieval fee.

### 4. S3 One Zone-Infrequent Access (One Zone-IA)

- **Description**: Stores data in a single AZ for lower cost.
- **Use Case**: Non-critical backups, easily re-creatable data.
- **Durability**: 99.999999999% (within one AZ)
- **Availability**: 99.5%
- **Cost**: Cheaper than Standard-IA.

### 5. S3 Glacier

- **Description**: Archival storage with retrieval times from minutes to hours.
- **Use Case**: Compliance archives, long-term backups.
- **Durability**: 99.999999999%
- **Retrieval time**: Expedited (1–5 min), Standard (3–5 hrs), Bulk (5–12 hrs)

### 6. S3 Glacier Deep Archive

- **Description**: Lowest-cost archival storage for rarely accessed data.
- **Use Case**: Legal archives, historical datasets accessed once or twice a year.
- **Durability**: 99.999999999%
- **Retrieval time**: 12–48 hours

---

## 🔹 Working with Amazon S3 (Bucket & Object Operations)

### Creating a Bucket

Steps (via Console):
1. Go to the [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)
2. Click **"Create bucket"**
3. Choose a globally unique name
4. Select AWS Region
5. Configure settings (versioning, encryption, etc.)
6. Click **Create**

### Uploading Objects

Steps:
1. Select your bucket → Click **Upload**
2. Add files or folders
3. Choose storage class, encryption, and permissions
4. Confirm and upload

---

## 🔹 Hosting a Static Website with Amazon S3

### 🛠 Steps to Host a Static Website

1. **Create a new bucket**: The bucket name must match your domain name (e.g., `myportfolio.com`).
2. **Upload static files**: Include `index.html` (home page) and `error.html` (error handler).
3. **Enable Static Website Hosting**: Under bucket **Properties**, enable and configure it by specifying index and error documents.
4. **Set Bucket Policy for Public Access**: Add the following JSON policy to allow public read access:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": ["s3:GetObject"],
    "Resource": ["arn:aws:s3:::myportfolio.com/*"]
  }]
}
