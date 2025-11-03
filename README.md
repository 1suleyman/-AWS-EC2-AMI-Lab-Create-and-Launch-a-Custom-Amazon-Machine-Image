# 🧩 AWS EC2 AMI Lab – Create and Launch a Custom Amazon Machine Image

In this lab, I learned how to **create a custom Amazon Machine Image (AMI)** from an existing EC2 instance.
The goal was to capture the full configuration and web server setup (including a custom NGINX page) so that any new instance launched from this AMI automatically serves the same webpage — saving setup time and enabling easy replication.

---

## 📋 Lab Overview

**Goal:**

* Understand what an Amazon Machine Image (AMI) is
* Create a custom AMI from an existing EC2 instance
* Launch a new EC2 instance using the custom AMI
* Verify that the new instance automatically serves the custom web page

**Learning Outcomes:**

* Navigate to the EC2 service and manage AMIs
* Create reusable golden images for automation
* Understand how AMIs capture system configuration, installed packages, and application files
* Launch new EC2 instances from custom AMIs

---

## 🛠 Step-by-Step Journey

### Step 1 – Log In to AWS Console

Used the provided credentials to access the AWS Management Console.
✅ Signed in successfully.

---

### Step 2 – Inspect Existing EC2 Instance

* Existing instance name: **EC2-AMI-LAB**
* Navigated to **EC2 → Instances → EC2-AMI-LAB**
* Opened **Security tab** and found:
  **Security Group ID:** ends in `52A`

✅ Confirmed instance details.

---

### Step 3 – Verify Custom Web Page on EC2 Instance

The NGINX package was already installed and modified with a custom HTML page.

To verify:

* Copied the **Public IP** of the instance (example: `3.10.192.10`)
* Opened `http://<public-ip>` in the browser

✅ The page displayed the custom message confirming NGINX is running.

---

### Step 4 – Create a Custom AMI from the Instance

**Details:**

* **Source instance:** EC2-AMI-LAB
* **Image name:** `ec2-kk-custom-ami`
* **Region:** us-east-1
* **All other settings:** Default

**Steps:**

1. Go to **EC2 → Instances → EC2-AMI-LAB**
2. Click **Actions → Image and templates → Create image**
3. Enter `ec2-kk-custom-ami`
4. Click **Create Image**

✅ New AMI created and status initially set to **Pending**.

---

### Step 5 – Verify AMI Status

* Navigated to **EC2 → AMIs**
* Monitored progress until **Status = Available**

✅ The AMI was successfully created and ready for use.

---

### Step 6 – Launch a New Instance Using the Custom AMI

**Details:**

* **Name:** `EC2-Custom-KK`
* **AMI:** `ec2-kk-custom-ami` (the one created earlier)
* **Instance Type:** `t2.micro`
* **Key Pair:** `ec2-kk-key` (existing)
* **Security Group:** `codecloud-sg` (previously created)
* **Storage:** 10 GiB, gp2

**Steps:**

1. Select **AMIs → ec2-kk-custom-ami → Launch instance from AMI**
2. Configure instance settings (VPC, subnet, security group, key pair)
3. Launch instance

✅ Instance launched successfully using the custom AMI.

---

### Step 7 – Verify Web Page from New Instance

* Copied the **Public IPv4 address** of the new instance
* Opened it in the browser using `http://<public-ip>`

✅ The custom NGINX web page loaded automatically, confirming that the AMI successfully preserved all configurations.

---

## 🏁 End of Lab

### ✅ Key Actions Summary

| Task                     | Action                                       |
| ------------------------ | -------------------------------------------- |
| Verify base EC2 instance | EC2 → Instances → EC2-AMI-LAB                |
| Confirm security group   | Security tab → Group ID ends in `52A`        |
| Test custom webpage      | Visit `http://<public-ip>`                   |
| Create AMI               | Actions → Image and templates → Create image |
| Verify AMI status        | EC2 → AMIs → Check “Available”               |
| Launch new instance      | Launch instance from custom AMI              |
| Verify webpage           | Visit new instance’s public IP               |

---

### 💡 Notes / Tips

* An **AMI (Amazon Machine Image)** is like a *snapshot* of your server configuration — including OS, packages, and data.
* Creating AMIs helps automate repetitive setup tasks for future deployments.
* You can share AMIs across accounts or regions for scaling production workloads.
* Always verify **AMI status = Available** before launching new instances.
* Use **descriptive AMI names** to keep track of environment versions.

---

### ✅ References

* [Amazon Machine Images (AMI) Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
* [AWS EC2 User Guide – Launching Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/LaunchingAndUsingInstances.html)
* [NGINX on Amazon Linux 2 Setup Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html)
