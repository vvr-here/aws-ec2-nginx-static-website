# 🌐 Deploying a Static Website on AWS EC2 Using NGINX

## 📌 Project Overview

This project demonstrates the deployment of a static website on an Amazon EC2 instance using NGINX as the web server.

The objective was to understand how a web server can be configured and made publicly accessible using AWS cloud infrastructure.

Instead of relying on fully managed website hosting services, I manually configured the EC2 instance, established an SSH connection through Windows PowerShell, installed NGINX, and configured AWS Security Groups to allow HTTP traffic.

This hands-on project helped me understand the fundamentals of cloud infrastructure, Linux server administration, web server deployment, and cloud networking.

## 🎯 Project Objectives

- Provision a virtual server using Amazon EC2.
- Establish a remote SSH connection using a `.pem` key pair.
- Install and configure NGINX on a Linux server.
- Deploy a custom static HTML webpage.
- Configure AWS Security Groups to allow HTTP traffic.
- Access the hosted webpage using the EC2 public IPv4 address.

## 🛠️ Technologies & Services Used

| Technology | Purpose |
|---|---|
| Amazon EC2 | Cloud-based virtual server |
| Linux | Server operating system |
| NGINX | Web server |
| SSH | Secure remote server access |
| Windows PowerShell | SSH client |
| AWS Security Groups | Virtual firewall |
| HTML | Static webpage content |

## 🏗️ Architecture

The deployment follows a simple client-server architecture.

```text
       Local Machine
     (Windows PowerShell)
              |
              | SSH - Port 22
              | .pem Key Pair
              ▼
       AWS EC2 Instance
         (Linux Server)
              |
              ▼
         NGINX Web Server
              |
              ▼
        /var/www/html/
              |
              ▼
         index.html

       Website Access Flow
              |
              ▼
        Client Browser
              |
              | HTTP - Port 80
              ▼
       AWS Security Group
              |
              ▼
         EC2 Instance
              |
              ▼
         NGINX Server
              |
              ▼
         Static Webpage
```

## ⚙️ Implementation Process

### Step 1: Launching an EC2 Instance

- Opened the AWS Management Console.
- Navigated to Amazon EC2.
- Launched a new EC2 instance.
- Selected a Linux-based Amazon Machine Image (AMI).
- Selected an instance type.
- Created and downloaded an SSH key pair in `.pem` format.
- Launched the instance and verified that its status was Running.

### Step 2: Connecting to EC2 Using SSH

Used Windows PowerShell to establish a remote connection to the EC2 instance.

SSH command:

```powershell
ssh -i "your-key.pem" ec2-user@YOUR_PUBLIC_IP
```

For Ubuntu instances, the default username is generally `ubuntu`.

This established a secure connection to the remote Linux server.

### Step 3: Installing NGINX

After connecting to the EC2 instance, installed the NGINX web server.

For Ubuntu:

```bash
sudo apt update
sudo apt install nginx -y
```

For Amazon Linux 2023:

```bash
sudo dnf update -y
sudo dnf install nginx -y
```

Started the NGINX service:

```bash
sudo systemctl start nginx
```

Enabled NGINX to start automatically after system reboots:

```bash
sudo systemctl enable nginx
```

Verified the service:

```bash
sudo systemctl status nginx
```

### Step 4: Deploying the Static Webpage

NGINX serves website files from its configured document root.

The default document root on common Ubuntu and Amazon Linux NGINX configurations is:

```bash
/var/www/html/
```

Created or edited the default HTML file:

```bash
sudo nano /var/www/html/index.html
```

Added custom HTML content and saved the file.

NGINX then served the webpage through HTTP requests.

### Step 5: Configuring AWS Security Groups

Configured the EC2 Security Group to allow the required inbound traffic.

| Type | Protocol | Port | Source | Purpose |
|---|---|---|---|---|
| SSH | TCP | 22 | My IP | Remote server access |
| HTTP | TCP | 80 | 0.0.0.0/0 | Public website access |

**Why these ports?**

- **Port 22 (SSH):** Allows secure remote administration of the EC2 instance.
- **Port 80 (HTTP):** Allows users to access the website through a web browser.

SSH access was intended for my IP address, while HTTP access was made publicly available.

### Step 6: Accessing the Deployed Website

After configuring NGINX and the Security Group:

1. Copied the EC2 instance's Public IPv4 address.
2. Opened a web browser.
3. Entered the public IP address using HTTP.

```text
http://YOUR_EC2_PUBLIC_IP
```

The browser successfully accessed the webpage hosted on the EC2 instance.

## 📸 Project Screenshots

### 1. NGINX Installation and Configuration

This screenshot demonstrates the NGINX setup on the EC2 Linux instance.

![NGINX Setup](screenshots/nginx-setup.png)

### 2. Static Website Deployment

This screenshot demonstrates the successfully deployed webpage accessed through the EC2 public IPv4 address.

![Website Deployment](screenshots/website-deployment.png)

## 📚 Key Learnings

Through this hands-on project, I gained practical knowledge of:

**1. Amazon EC2**
- Launching and managing virtual machines in AWS.
- Understanding EC2 instance states and public IPv4 addresses.
- Connecting cloud infrastructure to external clients.

**2. SSH and Remote Administration**
- Establishing SSH connections from Windows PowerShell.
- Understanding `.pem` key pairs.
- Managing remote Linux servers.

**3. Linux Server Administration**
- Installing software packages.
- Managing services using `systemctl`.
- Working with Linux directories and files.
- Understanding web server document roots.

**4. NGINX Web Server**
- Understanding the role of a web server.
- Installing and starting NGINX.
- Serving static HTML content.
- Understanding HTTP request and response handling.

**5. AWS Security Groups**
- Understanding virtual firewall configurations.
- Configuring inbound traffic rules.
- Learning the purpose of TCP ports 22 and 80.
- Understanding how network access is controlled in AWS.

**6. Cloud Networking Fundamentals**
- Understanding client-server communication.
- Learning how public IP addresses enable internet accessibility.
- Understanding the relationship between ports, firewall rules, and web servers.

## 🔍 Useful Commands

| Command | Purpose |
|---|---|
| `sudo apt update` | Updates Ubuntu package information |
| `sudo apt install nginx -y` | Installs NGINX on Ubuntu |
| `sudo systemctl start nginx` | Starts NGINX |
| `sudo systemctl enable nginx` | Enables automatic startup |
| `sudo systemctl status nginx` | Checks NGINX status |
| `sudo systemctl restart nginx` | Restarts NGINX |
| `sudo ss -tlnp` | Displays listening network sockets |
| `curl -I http://localhost` | Tests the local HTTP response |

## 🚀 Future Improvements

I plan to extend this project by exploring:

- **Terraform:** Automating EC2 provisioning and Security Group configuration.
- **Amazon Route 53:** Connecting a custom domain.
- **SSL/TLS:** Enabling HTTPS communication.
- **CI/CD:** Automating website deployment.
- **Amazon CloudWatch:** Monitoring server performance and logs.
- **AWS VPC:** Exploring subnets, route tables, internet gateways, and network ACLs.

## 👨‍💻 Author

**Vineet Vikram Rao**

Aspiring Cloud Network Engineer | AWS | Linux | Networking | Terraform

- GitHub: https://github.com/galac01389
- LinkedIn: https://linkedin.com/in/vvrao13

---

⭐ This project represents one of my hands-on steps toward understanding cloud infrastructure and networking.

**Project Status:** Successfully Completed

**Primary Focus:** AWS EC2 | NGINX | Linux | SSH | Cloud Networking
