# 🚀 AWS CLI – S3 Bucket Project

This project walks through configuring the AWS CLI with an IAM user, creating an S3 bucket, uploading a file, verifying the contents, and cleaning up—all from the command line.

It is designed to demonstrate practical cloud engineering skills:
- Working with **IAM** and secure credentials
- Using the **AWS CLI** instead of the console
- Managing **S3 buckets and objects**
- Following **best practices** (least privilege, cleanup, safe credential handling)

---

## 🌐 Environments & Technologies Used

- **Cloud Provider:** Amazon Web Services (AWS)
- **Services Used:**
  - IAM (Identity and Access Management)
  - S3 (Simple Storage Service)
  - STS (Security Token Service)
- **Tools:**
  - AWS CLI v2
  - Windows PowerShell

---

## 🖥 Operating System

- **Windows 11** (PowerShell terminal)

---

## 🧱 1. Prerequisites

Before starting:

1. An active **AWS account**
2. **AWS CLI v2** installed  
   - Verified with:
     ```bash
     aws --version
     ```
3. Basic familiarity with:
   - Running commands in a terminal
   - Navigating the AWS Management Console

---

## 🔐 2. Configure AWS CLI with IAM Credentials

### 2.1 Create an IAM User for CLI Access

1. In the AWS Console, go to **IAM → Users → Create user**
2. Set a username, for example:
   - `cli-user`
3. Attach permissions (for this learning project):
   - `AmazonS3FullAccess`  
     > In a real environment you would scope this down with least-privilege policies.

📸 **Screenshot 1 – IAM User Created (no secrets shown)**  
```md
![IAM User Created](screenshots/01-iam-user-created.png)
