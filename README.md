
---

# **Node.js CI/CD on AWS EC2 – Beginner DevOps Project**

## **Project Overview**

This project demonstrates a **full DevOps pipeline** for a Node.js application, from code commit to automatic deployment on an **AWS EC2 t3.micro instance** using **GitHub Actions**.

The goal is to showcase the **core DevOps practices**:

* Continuous Integration (CI) – automatic build and test on code changes.
* Continuous Deployment (CD) – automated deployment to a cloud server.
* Remote environment setup and management on AWS EC2.
* Secure, repeatable, and automated workflows using GitHub Actions.

This project is designed for beginners but illustrates **end-to-end DevOps practices**.

---

## **Key Features**

1. **AWS EC2 Instance Setup**

   * Launch and configure a t3.micro Linux instance.
   * Install Node.js, npm, and Git to run and manage the app.
   * Setup PM2 to run the Node.js app as a background process.

2. **Node.js Application**

   * A simple "Hello DevOps World" app, ready for automated builds and deployments.
   * Can be extended to full-stack or web applications.

3. **Version Control & GitHub Integration**

   * Code pushed to GitHub repository.
   * GitHub Actions workflow to automate CI/CD.

4. **GitHub Actions CI Pipeline**

   * Automatic build and test triggered on `main` branch push.
   * Steps include:

     * Checkout code
     * Node.js setup
     * Install dependencies (`npm install`)
     * Run build script (`npm run build`)
     * Run tests (`npm test`)

5. **Automated Deployment to EC2**

   * Secure SSH connection from GitHub Actions to EC2.
   * Private SSH key stored as GitHub Secret.
   * Commands executed via GitHub Actions:

     * Pull latest code from GitHub
     * Install dependencies
     * Start or restart app with PM2

6. **Testing the Full CI/CD Pipeline**

   * Any code push triggers build → test → deploy.
   * Verify deployment live on EC2 using PM2 logs and app output.

---

## **Project Structure**

```
my-node-app/
├─ index.js                # Main application file
├─ package.json            # Node.js app configuration
├─ package-lock.json
├─ .github/
│   └─ workflows/
│       └─ ci.yml          # GitHub Actions CI/CD workflow
├─ README.md               # Project documentation
```

---

## **Setup Instructions (for Beginners)**

### 1. Launch EC2 Instance

* Use AWS console → EC2 → t3.micro → Linux AMI → SSH enabled.

### 2. Connect to EC2

```bash
ssh -i my-key.pem ec2-user@<EC2_PUBLIC_IP>
```

### 3. Install Required Software

```bash
sudo yum update -y
sudo yum install -y nodejs npm git
sudo npm install -g pm2
```

### 4. Prepare SSH Keys for GitHub Actions

* Generate key pair locally.
* Add public key to EC2 `~/.ssh/authorized_keys`.
* Add private key as GitHub secret (`EC2_SSH_KEY`).

### 5. Set Up Node.js App

```bash
mkdir my-node-app
cd my-node-app
npm init -y
echo 'console.log("Hello DevOps World!")' > index.js
```

### 6. Push Code to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <repo-url>
git push -u origin main
```

### 7. Configure GitHub Actions Workflow

* `.github/workflows/ci.yml` to build, test, and deploy to EC2.
* Uses `appleboy/ssh-action` to SSH into EC2 and run PM2 commands.

### 8. Test Full Pipeline

* Make a code change → push to `main`.
* GitHub Actions automatically builds, tests, and deploys app.
* Check deployment on EC2 with:

```bash
pm2 list
pm2 logs
```

---

## **What You Learned in This Project**

* Launching and managing cloud servers (AWS EC2).
* Installing and configuring Node.js, npm, and Git on Linux.
* Writing a simple Node.js app and managing it with PM2.
* Using GitHub Actions to automate **CI/CD pipelines**.
* Securely deploying apps using SSH keys and repository secrets.
* Understanding the flow of **DevOps automation**: code → build → test → deploy.

---

## **Next Steps (Optional Enhancements)**

* Add **rollback** on failed deployments.
* Integrate **monitoring and logging** (e.g., CloudWatch, PM2 monitoring).
* Add **notifications** for pipeline success/failure (Slack, email).
* Extend to **multi-environment deployment** (dev/staging/prod).
* Add **unit and integration tests** for more advanced CI.

---

## **Conclusion**

This project demonstrates a **complete beginner-friendly DevOps workflow** that integrates cloud hosting, automated build/test, and deployment. It is **portfolio-ready**, showing practical knowledge of DevOps principles, cloud infrastructure, and CI/CD automation.

---
