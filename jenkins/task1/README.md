# 1st Task of Jenkins 

## Task overview
Install and connect with jenkins server
## Task Implementation
### 1️⃣ Access Jenkins Server
Login from the **jump host** to the Jenkins server:
```bash
ssh root@jenkins
```
2. System update
```bash 
yum update -y
```
3. Install Java 17 (Required for Jenkins)
```bash
yum install -y java-17-openjdk

```
4. Add Jenkins Repository and Key
```bash
yum install -y wget
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

```
5. Install Jenkins
```bash 
yum install -y jenkins
```

6. Enable and Start Jenkins Service
```bash
systemctl enable jenkins
systemctl start jenkins

```
7. check jenkins service
```bash 
systemctl status jenkins
```
8. Access Jenkins UI using the given jenkins tab
9. Retrieve the initial jenkins admin password:
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```
10. Install plugin
11. Provide the credentials when prompted with given adminuser, password, name and email address.
 This is all about install and connect with jenkins server