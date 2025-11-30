# Lab: Launching a Web Server on EC2

### 📋 Objective
Deploy a Linux EC2 instance and configure it to serve a simple HTML page using the Apache Web Server.

### ⚙️ Services Used
* **Amazon EC2** (t2.micro)
* **Security Groups** (Firewall configuration)
* **User Data** (Bootstrapping script)

### 🚀 Steps Taken
1.  **Network Setup:** Created a Security Group allowing **HTTP (80)** and **SSH (22)** traffic.
2.  **Instance Launch:** Launched a `t2.micro` instance using Amazon Linux 2023 AMI.
3.  **Bootstrapping:** Used the following User Data script to install Apache automatically:
    ```bash
    #!/bin/bash
    yum update -y
    yum install -y httpd
    systemctl start httpd
    systemctl enable httpd
    echo "<h1>Hello from AWS Lab!</h1>" > /var/www/html/index.html
    ```
4.  **Verification:** Accessed the instance Public IP in the browser and confirmed the page loaded.

### 💡 Key Learnings
* Learned that Security Groups are stateful (inbound rules automatically allow outbound traffic).
* Understood how User Data runs only during the first boot cycle.
