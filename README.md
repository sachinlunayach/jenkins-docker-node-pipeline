✅ Final README.md (Fully Professional)
markdown
Copy
Edit
# 🚀 Jenkins + Docker + Node.js Pipeline (Ubuntu EC2)

This project shows how to build a basic Jenkins Pipeline that runs inside a Docker container (`node:16-alpine`) to test Node.js in a clean and repeatable CI/CD process.

---

## 🧰 Requirements

- AWS EC2 instance (Ubuntu 20.04 or higher)
- Jenkins installed
- Docker installed
- Port 8080 open in the Security Group

---

## ⚙️ Step-by-Step Setup Guide

### ☁️ 1. Launch Ubuntu EC2 and Open Port 8080

- Open AWS EC2 Console
- Launch Ubuntu instance
- In **Security Group → Inbound Rules**, add:
  - Type: Custom TCP, Port Range: **8080**, Source: `0.0.0.0/0`

---

### ☕ 2. Install Java (Jenkins Requirement)

```bash
sudo apt update -y
sudo apt install openjdk-17-jdk -y
java -version
```
🐳 3. Install Docker
```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```
👷 4. Install Jenkins
```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y
sudo apt install jenkins -y
```
🔐 5. Allow Port 8080 (Firewall)
```bash
sudo ufw allow 8080
sudo ufw reload
```
Or make sure port 8080 is allowed in AWS Security Group.

🔄 6. Start and Enable Jenkins
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
Now access Jenkins in your browser:

http://<your-ec2-public-ip>:8080
🔑 7. Get Jenkins Admin Password
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password, paste it in the browser to unlock Jenkins.
```

🛠️ 8. Jenkins Dashboard Setup
Install Suggested Plugins

Create your admin user

Finish setup and go to Jenkins dashboard

🔧 9. Give Docker Permission to Jenkins
```bash
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
sudo systemctl restart docker
sudo systemctl restart jenkins
```
Then reboot the system:
```bash
sudo reboot
```
✅ This allows Jenkins to run Docker commands.

🧪 Clone and Connect GitHub Repo
📥 10. Clone This Repository (Optional for Local Testing)
```bash
git clone https://github.com/sachinlunayach/jenkins-docker-node-pipeline.git
cd jenkins-docker-node-pipeline
```
🔧 11. Create a Jenkins Pipeline Job (Not Freestyle)
Go to Jenkins dashboard → New Item

Enter a name: docker-node-pipeline

Select Pipeline → OK

Scroll to Pipeline → Definition: Select Pipeline script from SCM

Choose Git and paste this URL:
https://github.com/sachinlunayach/jenkins-docker-node-pipeline.git
Script Path: Jenkinsfile

Save → Click Build Now

✅ Pipeline Output
You should see output like:
+ node --version
v16.xx.x
🚀 Future Enhancements
Add stages like npm install, npm test

Build and push Docker images

Deploy to AWS, DockerHub, or any cloud

📎 References
Jenkins Docker Agents: https://www.jenkins.io/doc/book/pipeline/docker/

EC2 Setup Guide: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html

🙌 Author
Sachin Lunayach
GitHub: @sachinlunayach

📝 License
This project is licensed under the MIT License.
---

### 💾 Step 4: Save the File

If you used `nano`:
- Press `Ctrl + O` → Hit Enter → `Ctrl + X` to exit

---

### ✅ Step 5: View It on GitHub

Once pushed to your GitHub repo, your `README.md` will be beautifully rendered with:
- **Copy buttons** on code blocks
- Clickable links
- Cleanly organized sections

---

Would you like me to convert this into a downloadable `.md` or `.pdf` file or generate a Powe
