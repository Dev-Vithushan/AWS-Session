### **How to Access an EC2 Instance Using SSH**

Follow these steps to securely connect to your EC2 instance using SSH from your terminal or an SSH client:

---

#### **Step 1: Prerequisites**
1. **EC2 Instance**: Ensure you have a running EC2 instance.
2. **Key Pair**: Make sure you have the `.pem` file of the key pair associated with the instance.
   - The `.pem` file is generated when you create a key pair in AWS.
3. **Public IP Address or Public DNS**: Note down the public IP or DNS name of the instance.
4. **SSH Client**:
   - For macOS/Linux: Use the built-in terminal.
   - For Windows: Use PowerShell or a tool like PuTTY.

---

#### **Step 2: Set Up Key Permissions**
Ensure your private key file (`.pem`) has secure permissions. Run the following command:

```bash
chmod 400 <key-file>.pem
```

---

#### **Step 3: SSH into the EC2 Instance**
1. Use the following command to connect:

   ```bash
   ssh -i <key-file>.pem ec2-user@<public-ip-or-dns>
   ```

   Replace:
   - `<key-file>.pem` with the path to your `.pem` file.
   - `<public-ip-or-dns>` with your instance’s public IP or DNS name.
   - `ec2-user` with the appropriate user for the AMI:
     - **Amazon Linux**: `ec2-user`
     - **Ubuntu**: `ubuntu`
     - **CentOS**: `centos`
     - **Debian**: `admin` or `root`

2. Example:

   ```bash
   ssh -i my-key.pem ec2-user@3.123.45.67
   ```

---

#### **Step 4: Verify the Connection**
- Once connected, you should see a prompt indicating that you are inside the EC2 instance.

---

### **Troubleshooting Tips**
1. **Key File Issues**: Ensure the `.pem` file permissions are set to 400.  
2. **Firewall Rules**: Check the security group attached to the instance:
   - Allow inbound SSH traffic on port `22`.
   - Specify your IP in the rule or allow all (`0.0.0.0/0`) for testing (not recommended for production).  
3. **Public IP Issues**: Make sure you’re using the correct public IP or DNS and that the instance has an Elastic IP if required.  
4. **User Error**: Ensure you're using the correct username (`ec2-user`, `ubuntu`, etc.) for the AMI.
