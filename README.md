# CI/CD Project: To-Do Application

This project automates the deployment of a **To-Do Application** using **Jenkins**, **Docker**, and **GitHub**. It includes the steps to set up an EC2 instance, install Jenkins, and configure it for continuous integration and continuous delivery (CI/CD) to automatically build and deploy the application using Docker. We’ll also set up GitHub Webhooks to trigger Jenkins builds automatically when code is pushed to the repository.

---

### 🛠 **Technologies Used**

- **AWS EC2**: For hosting Jenkins and Docker containers.  
- **Jenkins**: To automate builds and deployments.  
- **Docker**: To containerize the application.  
- **GitHub**: For version control and repository hosting.  

---

### 🚀 **Deployment & Setup Instructions**

#### Step 1: **Set Up EC2 Instance**
1. Launch an EC2 instance with **Ubuntu** as the OS image.
2. SSH into your EC2 instance.

---

#### Step 2: **Install Jenkins on EC2 Instance**
1. **Update and Install Java and verify it** (Jenkins requires Java to run):  
   ```bash
   sudo apt update
   sudo apt install openjdk-17-jre
   java --version

---

#### Step 3: **Add Jenkins Repository and Install Jenkins**
1. **Run the following commands to install Jenkins**:  
   ```bash
   curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
   sudo apt-get install jenkins

---

#### Step 4: **Allow HTTP Traffic on Port 8080 and access Jenkins Web Interface**
1. Make sure the security group of your EC2 instance allows inbound traffic on port 8080.
2. Open your browser and access Jenkins by navigating to http://(your-ec2-public-ip):8080

---

#### Step 5: **Fetch Jenkins Admin Password**
1. Run the following command to retrieve the initial Jenkins admin password:  
   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
2. Copy the password and paste it in the Jenkins web interface to complete the setup

---

#### Step 6: **Configure Jenkins for GitHub Integration**
1. **Create a New Jenkins Job**:  
   Navigate to Jenkins dashboard → **New Item** → Enter job name → Select **Freestyle project**.
2. **Connect GitHub Repo**:
   If your repository is public, simply add the GitHub repository URL under the **Source Code Management** section.
   If your repository is private, generate an SSH key:
   ```bash
   ssh-keygen
   ```
   Add the `id_rsa.pub key` (public key) to your GitHub account's SSH keys.
   Add the private key (`id_rsa`) in the Credentials section of Jenkins.
3. **Build the Application**:
   After setting up the GitHub repository in Jenkins, click **Build Now** to test if the Jenkins job can pull the repository and create the app directory.

---

#### Step 7: **Install Docker on EC2 Instance**
1. Install Docker:
Run the following command to install Docker:
   ```bash
   sudo apt install docker.io
2. Add Ubuntu User to Docker Group:
   ```bash
   sudo usermod -a -G docker $USER
   sudo reboot
3. Create Dockerfile for Application

---

#### Step 8: **Automate Docker Container Execution with Jenkins**
1. **Create a New Jenkins Job**:  
   Go to Jenkins Job → **Configure** → **Add Build Step** → Select **Execute Shell**.
2. Add Docker Build and Run Commands:
   ```bash
   docker build . -t todo-app
   docker run -d --name node-todo-app -p 8000:8000 todo-app
3. If you face permission issues while building the pipeline, execute the following on you ec2 linux terminal:
   ```bash
   sudo usermod -a -G docker jenkins
   sudo systemctl restart jenkins
4. Build the Pipeline

---

#### Step 9: **Set Up GitHub Webhook for Automatic Deployments**
1. Install the **GitHub Integration** plugin in Jenkins to automate triggers from GitHub.
2. Add the SSH key in Jenkins (similar to how it was done in **Step 6**).
3. Go to your GitHub repository → Settings → Webhooks → Add webhook.
4. Set the Payload URL to the Jenkins server URL (e.g., `http://(your-ec2-public-ip):8080/github-webhook/`).
5. Set the Content type to `application/json`.
6. Set Events to `push` to trigger Jenkins builds when code is pushed to GitHub.

   




