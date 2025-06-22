# Create an AWS Lambda function that automatically stops your Linux-based EC2 instance using a trigger (e.g., scheduled via CloudWatch Events):

---

### ✅ Step-by-Step: Lambda to Stop EC2 Instance

---

### **Step 1: Create IAM Role for Lambda**

1. Go to **IAM → Roles** → **Create role**
2. Select **Trusted Entity**: Choose `AWS service`
3. Use case: **Lambda**
4. Click **Next** → Attach the following policies:

   * `AmazonEC2FullAccess` (or better: create a custom policy with `ec2:StopInstances`)
   * `CloudWatchLogsFullAccess` (to view logs)
5. Name the role: `lambda-stop-ec2-role`
6. Click **Create role**

---

### **Step 2: Create the Lambda Function**

1. Go to **AWS Lambda** → **Create Function**
2. Choose:

   * Author from scratch
   * Name: `StopEC2InstanceLambda`
   * Runtime: `Python 3.12` (or any supported runtime)
   * Permissions: Choose existing role → Select `lambda-stop-ec2-role`
3. Click **Create Function**

---

### **Step 3: Add Python Code to Stop EC2**

Paste the following code:

```python
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    instance_id = 'i-0abcdef1234567890'  # Replace with your instance ID

    response = ec2.stop_instances(InstanceIds=[instance_id])
    print(f"Stopping instance: {instance_id}")
    return response
```

✅ **Click Deploy** after updating the code.

---

### **Step 4: Create a Trigger (Scheduled)**

1. In the Lambda page → Click **Add Trigger**
2. Choose **EventBridge (CloudWatch Events)**
3. Select **Create a new rule**

   * Name: `stop-ec2-schedule`
   * Schedule expression: e.g. `cron(0 18 * * ? *)` (this stops at 6:00 PM UTC daily)
   * Description: `Daily EC2 shutdown`
4. Click **Add**

---

### **Step 5: Test the Lambda (Optional)**

1. Click **Test** in Lambda
2. Configure a new test event (any JSON, since no input is required)
3. Click **Test**

You should see `Stopping instance: i-0abcdef1234567890` in the logs.

---

### ✅ Summary

* Lambda runs with `AmazonEC2FullAccess`
* It targets the specific EC2 instance ID
* Triggered via EventBridge cron schedule
* Works even if instance is in a private subnet

