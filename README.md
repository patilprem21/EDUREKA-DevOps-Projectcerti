# DevOps CI/CD Pipeline Project - AppleBite Co.

This project implements a complete CI/CD pipeline for AppleBite Co. using Jenkins, Docker, Ansible, and Git as per the project statement requirements.

## 🎯 Project Objective

Create a CI/CD pipeline that automatically deploys code to dev, stage, or prod environments with just a single button click.

## 🏗️ Architecture

- **Master VM**: Jenkins Server with Ansible and Git
- **Slave Node**: Test Server (fresh instance) for deployment
- **Tools**: Git, Jenkins, Docker, Ansible

## 📋 Pipeline Jobs

### Job 1: Install Puppet Agent
- Installs and configures Puppet agent on the slave node (test server)

### Job 2: Install Docker via Ansible
- Uses Ansible to install Docker on the test server
- Configures Docker daemon and services

### Job 3: Deploy PHP Application
- Clones the PHP application from Git repository
- Builds and deploys the Docker container
- Deploys to port 8081

### Job 4: Container Cleanup (Automatic)
- If Job 3 fails, automatically cleans up running containers
- Ensures clean state for next deployment

## 🚀 Quick Start

### Prerequisites
- Docker Desktop installed and running
- Git installed
- Access to internet

### Setup Instructions

1. **Start the Environment**
   ```bash
   docker-compose up -d
   ```

2. **Access Jenkins**
   - URL: http://localhost:8082
   - Admin Password: Check Jenkins logs

3. **Configure Pipeline**
   - Create new Pipeline job
   - Use Jenkinsfile from SCM
   - Set repository to your Git repo

4. **Run Pipeline**
   - Click "Build Now"
   - Monitor execution

## 📁 Project Structure

```
EDUREKA-DevOps-Projectcerti/
├── ansible/
│   ├── install-docker.yml    # Docker installation playbook
│   ├── inventory             # Ansible inventory
│   └── ansible.cfg           # Ansible configuration
├── Jenkinsfile               # Jenkins pipeline definition
├── docker-compose.yml        # Container orchestration
└── README.md                 # This file
```

## 🔧 Configuration

### Ansible Configuration
- Host: test-server
- User: root
- Password: password
- Connection: SSH via Paramiko

### Jenkins Configuration
- Port: 8082
- Workspace: /var/jenkins_home/workspace/DevOps-Pipeline
- Ansible integration: Mounted volume

### Test Server Configuration
- Port: 8081
- Base Image: Ubuntu 20.04
- SSH: Enabled for Ansible connections

## 🧪 Testing

- **Jenkins**: http://localhost:8082
- **PHP Application**: http://localhost:8081
- **Test Server**: Accessible via SSH

## 🚨 Troubleshooting

1. **Docker Service Issues**: Check container logs
2. **Ansible Connection**: Verify SSH configuration
3. **Pipeline Failures**: Check Jenkins console output

## 📚 References

- **Original Project**: https://github.com/edureka-devops/projCert.git
- **PHP Base Image**: devopsedu/webapp
- **Project Statement**: See final project statement.txt

## 👨‍💻 Developer

**Premanand Patil** - DevOps Engineer
- GitHub: @patilprem21
- Email: pprem2802@gmail.com

---

⭐ **This project fulfills all requirements from the project statement and demonstrates a complete DevOps CI/CD pipeline implementation.**
