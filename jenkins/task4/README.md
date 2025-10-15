# Task 4 of Jenkins
## Task Overview
The DevOps team at **xFusionCorp Industries** is standardizing the Jenkins job structure to make it more organized and manageable.  
This task involves creating a dedicated folder within Jenkins and moving existing jobs into it.

---

## 🎯 Task Objectives
1. Access Jenkins using the provided credentials.  
2. Create a **folder named `Apache`** in Jenkins.  
3. Move the existing jobs:
   - `httpd-php`
   - `services`
   into the newly created `Apache` folder.
4. Install any necessary plugins (such as the *Folders Plugin*) and restart Jenkins if required.

---

## 🧩 Steps Performed

### 1. Access Jenkins
- Click on the **Jenkins** button from the top navigation bar.  
- Log in using the credentials:

## Task Implementation

---

### 2. Install Required Plugin
To manage jobs within folders, Jenkins requires the **Folders Plugin**.

- Go to: **Manage Jenkins → Plugins → Available plugins**
- Search for **Folders Plugin**
- Select and install it.
- Once installation completes, choose **“Restart Jenkins when installation is complete and no jobs are running.”**

---

### 3. Create a Folder
- Navigate to the Jenkins dashboard.
- Click **“New Item.”**
- Enter the name: **Apache**
- Select **Folder** as the item type.
- Click **OK**.
- (Optional) Add a description for clarity, e.g.,  
*“This folder contains Jenkins jobs related to Apache web services.”*

---

### 4. Move Existing Jobs into the Folder
- From the Jenkins dashboard:
- Hover over each job (`httpd-php` and `services`).
- Click the dropdown arrow → **Move**.
- Choose the destination folder: **Apache**.
- Confirm the move.

Alternatively:
- Go to **Dashboard → Apache folder**.
- Click **Move** and select the destination manually.

---

### 5. Verify Folder Structure
After completing the steps:
- Go to the Jenkins **Dashboard**.
- Confirm the following structure:

