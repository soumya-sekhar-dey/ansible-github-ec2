# 📦 Containerized Python Web App Deployment with Ansible & GitHub Actions

This project automates the deployment of a containerized Python web application to an AWS EC2 instance using **Ansible playbooks**. The deployment pipeline is integrated with **GitHub Actions** for seamless CI/CD automation.

---

## 📌 Project Overview

- **Build a Python web application Docker image**
- **Push the image to Docker Hub**
- **Deploy the application to a remote EC2 instance using Ansible**
- **Automate the deployment via GitHub Actions**

---

## 📚 Tech Stack

- **Ansible** — Configuration management and automation tool  
- **Docker** — Containerization platform for packaging the Python web app  
- **AWS EC2** — Virtual server to host the containerized app  
- **GitHub Actions** — CI/CD workflow automation  
- **Docker Hub** — Container image registry  

---

## 📁 Project Structure
ansible-github-ec2/ ├── ansible/ │ ├── inventory # Ansible inventory file (parameterized for EC2) │ ├── playbook.yml # Main Ansible playbook for deployment │ ├── ansible.cfg # Optional config to define inventory location and defaults │ └── id_rsa # SSH private key (should be ignored via .gitignore) ├── app/ │ └── app.py # Sample Python web application │ └── Dockerfile # Dockerfile for the web app ├── .github/ │ └── workflows/ │ └── deploy.yml # GitHub Actions CI/CD workflow file ├── .gitignore ├── README.md └── requirements.txt


---

## ⚙️ How It Works

1. **GitHub Actions workflow** triggers on code push
2. **Builds the Docker image** for the Python web app
3. **Pushes the image to Docker Hub**
4. **Runs an Ansible playbook** using `dawidd6/action-ansible-playbook` GitHub Action
5. **Ansible connects to EC2** using SSH and:
   - Pulls the Docker image
   - Runs the container
   - Maps port 5000 for external access

---

## 🔐 Security

- **SSH private keys** are managed securely via **GitHub Secrets**  
- **EC2 IP addresses** can be parameterized via **GitHub Secrets** or workflow variables  
- **Sensitive files like `id_rsa`** are excluded from version control using `.gitignore`

---

## 🚀 Deployment Instructions

### 1️⃣ Configure GitHub Secrets

In your GitHub repository, add these secrets:

| Secret Name        | Purpose                                  |
|:------------------|:------------------------------------------|
| `SSH_PRIVATE_KEY`  | Your EC2 instance SSH private key (contents) |
| `EC2_PUBLIC_IP`    | Public IP address of your EC2 instance      |
| `DOCKERHUB_USERNAME` | Your Docker Hub username                  |
| `DOCKERHUB_TOKEN`  | Docker Hub access token or password        |

---

### 2️⃣ Update Inventory File (Optional)

If not using secrets, manually update `ansible/inventory`:

```ini
[webserver]
ec2-instance ansible_host=YOUR_EC2_IP ansible_user=ec2-user ansible_ssh_private_key_file=ansible/id_rsa

📊 Outcome
✔️ Automated end-to-end deployment
✔️ No manual SSH into servers
✔️ CI/CD-driven container deployment pipeline
✔️ Infrastructure as Code via Ansible

📄 Author
Soumya Sekhar Dey
DevOps & Cloud Engineer