Here’s a **step-by-step guide** to create an **EC2 instance in AWS** using the AWS Management Console:

---

## 🧾 Step-by-Step: Launch an EC2 Instance on AWS

---

### ✅ Step 1: Log in to AWS Console

1. Go to [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
2. Sign in with your AWS account.

---

### ✅ Step 2: Go to EC2 Dashboard

1. In the **AWS Services** search bar, type and click **“EC2”**.
2. You’ll be taken to the **EC2 Dashboard**.

---

### ✅ Step 3: Launch a New EC2 Instance

1. Click **“Launch Instance”**.
2. Enter:

   * **Name**: e.g., `my-ec2-demo`
   * **Application and OS Image (AMI)**:

     * Select **Amazon Linux 2** (or Ubuntu, depending on your need).
   * **Instance type**: Choose `t2.micro` (Free Tier eligible).
   * **Key pair (login)**:

     * If you have one, select it.
     * Or, click **Create new key pair** → name it → download `.pem` file.

---

### ✅ Step 4: Configure Network Settings

1. **Network settings**:

   * VPC: default
   * Subnet: choose a default one
   * Auto-assign public IP: **Enable**
   * Firewall:

     * Check “Allow SSH traffic from” → Anywhere (`0.0.0.0/0`)
     * (Add HTTP if running a web server)

---

### ✅ Step 5: Add Storage (Optional)

* Default is **8 GiB** (Amazon Linux/Ubuntu) – you can keep it or increase as needed.

---

### ✅ Step 6: Launch Instance

1. Click **Launch Instance**.
2. Wait for the status → Should say **Running**.

---

### ✅ Step 7: Connect to Your Instance

1. Click on your instance name to open details.
2. Click **Connect** (top right) → Choose **SSH Client**.
3. Follow instructions:

   ```bash
   chmod 400 your-key.pem
   ssh -i "your-key.pem" ec2-user@your-public-ip
   ```

   * For Ubuntu, use `ubuntu@your-public-ip`

---

### ✅ Step 8: Install or Run Apps (Optional)

Once inside the instance via SSH, you can:

```bash
sudo yum update -y          # For Amazon Linux
sudo apt update             # For Ubuntu
```

Install web servers, applications, etc.

---

