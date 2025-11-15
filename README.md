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

<img width="1909" height="682" alt="1 - CLI USER CREATED " src="https://github.com/user-attachments/assets/bc27340a-37d3-4d52-b30b-4add7edd684d" />



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

<img width="1589" height="608" alt="2  set permission  " src="https://github.com/user-attachments/assets/57d7d02b-814f-450f-91ba-c6b0878ed5db" />

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

<img width="731" height="253" alt="3   STEP 7 — Verify the AWS CLI is Authenticated" src="https://github.com/user-attachments/assets/3999e239-353f-49dd-977d-e5b218157131" />

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

<img width="549" height="130" alt="4  s3 bucket made" src="https://github.com/user-attachments/assets/bd1ba3a3-0b7b-437d-834f-dac3ccedf4d0" />

---

### 3.3 Verify the Bucket Exists

To confirm successful creation, a list of all S3 buckets in the account was retrieved.  
The newly created bucket should appear in this list alongside any other existing buckets.

**What this verification confirms:**
- The AWS CLI is authenticated correctly  
- The bucket was created in your account  
- Your IAM permissions are working as intended  

<img width="627" height="242" alt="5 - VERIFY BUCKET EXERCISE 3" src="https://github.com/user-attachments/assets/6f6699f7-ff88-4c1c-9846-b7d890c162b5" />

## 📄 4. Upload a File to the S3 Bucket

This section demonstrates how to create a local file, upload it into the S3 bucket using the AWS CLI, and verify that the upload was successful by listing the objects stored in the bucket.

---

### 4.1 Create a Local Test File

A simple text file was created locally to serve as the object to upload into the S3 bucket.

**Steps performed:**
- Opened PowerShell in the working directory
- Created a file named **test.txt**
- Added sample content into the file for demonstration purposes

This file will be uploaded to the S3 bucket created in Section 3.

<img width="814" height="234" alt="6  CREATE TEST FILE" src="https://github.com/user-attachments/assets/3ea8925a-db37-46f4-a527-7eac6c0426e0" />


---

### 4.2 Upload the File to the S3 Bucket

With the local file created, the next step is to upload it to the bucket:

- The upload is performed entirely through the AWS CLI  
- The file is stored at the bucket’s root level  
- Successful uploads return confirmation in the terminal

<img width="789" height="151" alt="7  VERIFY TEST FILE EXIST" src="https://github.com/user-attachments/assets/ee0ac604-3b86-4a5c-9660-d73bfef1e2ed" />

---

### 4.3 Verify the File Exists in the Bucket

After uploading, the contents of the bucket were listed to verify that the object was successfully stored in S3.

**What this verification confirms:**
- The upload operation was successful
- The file exists inside your bucket
- Your IAM permissions allow object-level access
- The AWS CLI is communicating correctly with S3

## 🧹 5. Clean Up: Remove the S3 Object and Delete the Bucket

This final section demonstrates good cloud hygiene by removing the uploaded object and deleting the S3 bucket when the project is complete.  
Cleaning up ensures you avoid unnecessary AWS resource usage and keeps your environment organized.

---

### 5.1 Delete the File from the S3 Bucket

Before deleting the bucket itself, all objects inside it must be removed.  
In this step, the previously uploaded `test.txt` file is deleted.

**Why this step matters:**
- S3 buckets cannot be deleted while they contain objects
- This demonstrates safe object-level operations in S3
- Helps avoid incurring storage charges

📸 **Screenshot 9 – S3 Object Deleted (CLI output)**  


---

### 5.2 Delete the S3 Bucket

With the bucket empty, the next step is to delete the bucket itself.

<img width="652" height="97" alt="8 - CLEAN UP" src="https://github.com/user-attachments/assets/d0d2acf3-9ab4-43b5-a18d-997e1c5d2cf7" />


**Steps performed:**
- Ran the AWS CLI command that removes the bucket
- Confirmed the command forces deletion even if versions or markers exist
- Verified that the bucket was removed successfully

**Why this step matters:**
- Demonstrates full resource lifecycle management  
- Ensures no lingering AWS resources remain after testing  
- Reinforces responsible cloud usage practices  

## 🎓 6. Learning Outcomes & Conclusion

This project provided hands-on experience with configuring the AWS CLI, authenticating via IAM, working with S3 buckets, uploading and verifying objects, and responsibly cleaning up AWS resources.  
All tasks were performed entirely through the command line to simulate real cloud engineering workflows.

---

### 🎯 Key Learning Outcomes

Through this project, the following skills and concepts were practiced and reinforced:

#### **AWS Identity & Access Management (IAM)**
- Creating and configuring an IAM user for programmatic access  
- Understanding least-privilege principles  
- Working with Access Keys securely (never exposing the Secret Access Key)

#### **AWS CLI Fundamentals**
- Installing and configuring AWS CLI locally  
- Storing credentials securely on the client machine  
- Executing AWS service commands through PowerShell  

#### **AWS STS (Security Token Service)**
- Verifying current IAM identity  
- Ensuring authentication and permissions are functioning correctly  

#### **Amazon S3 Operations**
- Creating globally unique S3 buckets  
- Uploading objects to S3  
- Listing and verifying bucket contents  
- Removing objects and deleting buckets  
- Understanding the lifecycle of S3 resources  

#### **Cloud Hygiene & Best Practices**
- Cleaning up unused cloud resources  
- Avoiding unexpected storage charges  
- Keeping AWS accounts organized and minimal  

---

### 🧠 Overall Project Benefits

By completing this project, I demonstrated the ability to:

- Work with AWS using only the command line  
- Understand and manage cloud permissions  
- Perform object storage operations without the AWS Console  
- Follow secure credential-handling practices  
- Document cloud processes in a clear, educational format  
- Execute end-to-end cloud workflows independently  

These skills form the foundation for more advanced cloud engineering tasks, including automation, scripting, Infrastructure as Code, DevOps pipelines, and multi-service AWS projects.

---

### 🏁 Conclusion

This project successfully walked through the complete lifecycle of interacting with Amazon S3 using the AWS CLI—from IAM configuration to bucket creation, file uploads, verification, and cleanup.  
It demonstrates practical, real-world cloud engineering proficiency and builds confidence in using AWS services programmatically.

The combination of hands-on tasks, CLI-focused workflows, and secure operational practices reflects essential skills needed in modern Cloud and DevOps roles.

---


