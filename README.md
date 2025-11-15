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

This section covers the full process of creating an IAM user for CLI access, generating secure credentials, configuring the AWS CLI locally, and verifying that authentication is working correctly.  
Each step includes clear explanations and screenshot placeholders to document the process.

---

### 2.1 Create an IAM User for CLI Access

1. In the AWS Console, navigate to **IAM → Users → Create user**.
2. Assign a username, for example:
   - `cli-user`
3. Attach permissions (for this learning project):
   - `AmazonS3FullAccess`  
     > In real production environments, you would assign only the minimum required permissions.

📸 **Screenshot 1 – IAM User Created (no secrets shown)**  


---

### 2.2 Create an Access Key for the IAM User

To allow the AWS CLI to authenticate as this user, an access key must be generated.

**Steps performed:**
- Open the newly created **cli-user** inside the IAM console.
- Select the **Security credentials** tab.
- Scroll to **Access keys**.
- Click **Create access key**.
- Select **Command Line Interface (CLI)** as the use case.
- Download the `.csv` file containing the Access Key ID and Secret Access Key.  
  *(The secret key is never shown publicly or stored in GitHub.)*

📸 **Screenshot 2 – Access Key Created (Access Key ID only, no secret key)**  


---

### 2.3 Configure the AWS CLI Locally

The AWS CLI must be configured on your machine so that commands can be executed on behalf of the IAM user.

**Steps performed:**
- Open **Windows PowerShell**.
- Started the configuration process using the `aws configure` command.
- Entered the following when prompted:
  - **AWS Access Key ID**  
  - **AWS Secret Access Key**  
  - **Default region:** `us-east-1`  
  - **Default output format:** `json`
- Verified that the credentials were stored securely in your local AWS configuration directory.

> 📝 *This step is not screenshotted because it involves sensitive credential input.*

---

### 2.4 Verify AWS CLI Authentication

Once configuration was completed, authentication was verified by requesting the caller identity using AWS STS (Security Token Service).

**Steps performed:**
- Ran the identity verification command.
- Confirmed that the IAM user information appeared correctly:
  - User ARN  
  - AWS Account ID  
  - IAM User ID  
- This output contains no sensitive information and is safe to include in documentation.

📸 **Screenshot 3 – STS Caller Identity (safe to upload)**  

## 🪣 3. Create an S3 Bucket Using the AWS CLI

This section covers the process of creating a globally unique S3 bucket from the command line and confirming that the bucket exists within your AWS account.

---

### 3.1 Choose a Globally Unique Bucket Name

S3 bucket names must follow AWS naming rules:
- All lowercase  
- No spaces  
- Must be globally unique  
- Can include hyphens  

For this project, the bucket name used was:

- `dansosa-s3-bucket-0001`

This ensures compatibility across all AWS regions and services.

---

### 3.2 Create the S3 Bucket

Using the AWS CLI, the bucket was created with a single command.  
This action provisions a new S3 bucket in the default region configured earlier (`us-east-1`).

📸 **Screenshot 4 – S3 Bucket Created (CLI output)**  


---

### 3.3 Verify the Bucket Exists

To confirm successful creation, a list of all S3 buckets in the account was retrieved.  
The newly created bucket should appear in this list alongside any other existing buckets.

**What this verification confirms:**
- The AWS CLI is authenticated correctly  
- The bucket was created in your account  
- Your IAM permissions are working as intended  

📸 **Screenshot 5 – List of S3 Buckets (includes new bucket)**  

