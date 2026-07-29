# 🚀 DevOps CI/CD Pipeline Project using Jenkins, Docker & GitHub

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline** for deploying a static website using **GitHub, Jenkins, Docker, and AWS EC2**. Whenever changes are pushed to the GitHub repository, Jenkins automatically builds a Docker image and deploys the latest version of the website.

---

# 🛠️ Tech Stack

- AWS EC2 (Ubuntu Server 24.04 LTS)
- Jenkins
- Docker
- Git
- GitHub
- Apache2
- GitHub Webhooks
- Linux

---

# 📂 Project Architecture

```text
Developer
    │
    │ Git Push
    ▼
GitHub Repository
    │
    │ Webhook
    ▼
Jenkins Master
    │
    │ Build Docker Image
    │ Run Docker Container
    ▼
Website Running on Port 5000

(Optional)

Jenkins Master
      │
      │ SSH
      ▼
Jenkins Agent (Slave)
      │
      ▼
Distributed Build
```

---

# 🖥️ Infrastructure

| Server | Purpose |
|---------|---------|
| Dev Server | Prepare application and push code to GitHub |
| Jenkins Master | CI/CD automation, build Docker image, deploy application |
| Jenkins Agent | Execute distributed build jobs |

---

# 📁 Project Workflow

## Step 1 - Download Website

```bash
cd /root

wget https://www.tooplate.com/zip-templates/2130_waso_strategy.zip

apt-get update -y

apt install unzip -y

unzip 2130_waso_strategy.zip
```

---

## Step 2 - Create Dockerfile

```Dockerfile
FROM ubuntu

RUN apt-get update -y

RUN apt-get install -y apache2

COPY . /var/www/html

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

---

## Step 3 - Push Source Code to GitHub

```bash
git init

git add *

git commit -m "Initial commit Waso Strategy Website"

git remote add origin https://github.com/<your-username>/webserver-repo.git

git push -u origin master
```

---

# ⚙️ Jenkins Installation

Install Java

```bash
apt update -y

apt install fontconfig openjdk-21-jre -y
```

Install Jenkins

```bash
wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | tee /etc/apt/sources.list.d/jenkins.list

apt update -y

apt install jenkins -y
```

Start Jenkins

```bash
systemctl start jenkins
```

---

# 🐳 Docker Installation

```bash
apt install docker.io -y

systemctl start docker

systemctl enable docker
```

---

# 🔐 Jenkins Sudo Permission

Edit sudoers file

```bash
vim /etc/sudoers
```

Add

```text
jenkins ALL=(ALL) NOPASSWD: ALL
```

---

# 🔗 Configure GitHub Webhook

Navigate to

```
Repository
   ↓
Settings
   ↓
Webhooks
   ↓
Add Webhook
```

Payload URL

```
http://<Jenkins-Public-IP>:8080/github-webhook/
```

Content Type

```
application/json
```

---

# ⚙️ Jenkins Job Configuration

Create a Freestyle Project.

### Source Code Management

```
Git
```

Enter GitHub Repository URL.

---

### Build Trigger

Enable

```
GitHub hook trigger for GITScm polling
```

---

### Build Step

Execute Shell

```bash
sudo docker rm -f container1 || true

sudo docker build -t webserver-image .

sudo docker run -itd \
--name container1 \
-p 5000:80 \
webserver-image
```

---

# 🌐 Access Website

```
http://<Jenkins-Public-IP>:5000
```

---

# 🔄 Continuous Deployment

Whenever the developer updates the application,

```bash
vim index.html

git add *

git commit -m "Updated Website"

git push origin master
```

GitHub automatically sends a webhook to Jenkins.

Jenkins then:

- Clones latest code
- Builds Docker image
- Removes old container
- Starts new container
- Deploys updated website

No manual deployment is required.

---

# 👨‍💻 Jenkins Agent (Slave)

Install

```bash
apt update -y

apt install fontconfig openjdk-21-jre -y

apt install git -y

apt install docker.io -y

systemctl start docker

systemctl enable docker
```

The Jenkins Agent can be connected to the Jenkins Master for distributed builds and improved scalability.

---

# 🔄 CI/CD Pipeline Flow

```text
Developer

    │

Git Add

    │

Git Commit

    │

Git Push

    │

GitHub Repository

    │

GitHub Webhook

    │

Jenkins Build Trigger

    │

Clone Repository

    │

Docker Build

    │

Docker Run

    │

Deploy Website

    │

Application Available on Port 5000
```

---

# 📈 Features

- Automated CI/CD Pipeline
- GitHub Integration
- Dockerized Application
- Automatic Deployment
- GitHub Webhook Trigger
- Apache Web Server
- Linux Environment
- Jenkins Freestyle Project
- Scalable Build Architecture using Jenkins Agent

---

# 🎯 Learning Outcomes

Through this project, I gained practical experience in:

- Git Version Control
- GitHub Repository Management
- Jenkins Installation and Configuration
- Docker Image Creation
- Docker Container Management
- GitHub Webhooks
- Continuous Integration (CI)
- Continuous Deployment (CD)
- Linux Administration
- AWS EC2 Management

---

# 📷 Output

Application URL

```
http://<Jenkins-Public-IP>:5000
```

After every Git push, the latest version of the website is automatically deployed.

---

# 👨‍💻 Author

**YASH PARDE**

AWS | DevOps | Docker | Jenkins | Git | Linux | CI/CD
