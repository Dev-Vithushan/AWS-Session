### **Task: Simple Lambda Trigger on S3 Upload**  
In this task, you'll create an AWS Lambda function that is triggered whenever a file is uploaded to a specific S3 bucket. The Lambda function will log the file details (e.g., file name and size) to Amazon CloudWatch Logs.

---

### **Steps to Complete the Task**

---

#### **Step 1: Create an S3 Bucket**  
1. Go to the **S3 Console** and create a new bucket.
   - Name the bucket (e.g., `lambda-s3-trigger-demo`).
   - Leave other settings as default.

---

#### **Step 2: Create a Lambda Function**  
1. Go to the **Lambda Console** and click **Create Function**.
2. Select **Author from scratch**:
   - Function name: `S3FileLogger`.
   - Runtime: Select Python 3.x or Node.js.
3. Click **Create Function**.

---

#### **Step 3: Write the Lambda Function Code**  
For **Python**, use the following code:  

```python
import json

def lambda_handler(event, context):
    # Log the event details
    print("Event: ", json.dumps(event))
    
    # Extract bucket name and file name from the event
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    file_name = event['Records'][0]['s3']['object']['key']
    file_size = event['Records'][0]['s3']['object']['size']
    
    print(f"File uploaded: {file_name}, Size: {file_size} bytes, Bucket: {bucket_name}")
    
    return {
        'statusCode': 200,
        'body': json.dumps('File details logged successfully!')
    }
```

For **Node.js**, use the following code:  

```javascript
exports.handler = async (event) => {
    console.log("Event: ", JSON.stringify(event));
    
    const bucketName = event.Records[0].s3.bucket.name;
    const fileName = event.Records[0].s3.object.key;
    const fileSize = event.Records[0].s3.object.size;
    
    console.log(`File uploaded: ${fileName}, Size: ${fileSize} bytes, Bucket: ${bucketName}`);
    
    return {
        statusCode: 200,
        body: JSON.stringify('File details logged successfully!')
    };
};
```

Save the code and deploy the function.

---

#### **Step 4: Set Up S3 Trigger**  
1. In the Lambda function's **Configuration**, go to the **Triggers** tab and click **Add Trigger**.
2. Select **S3** as the trigger source.
3. Configure the trigger:
   - Bucket: Select your bucket (`lambda-s3-trigger-demo`).
   - Event type: Select **PUT** (for object creation).
   - Prefix/Suffix: Leave blank (or specify if needed).
4. Click **Add**.

---

#### **Step 5: Test the Setup**  
1. Upload a file to the S3 bucket via the AWS Console.
2. Go to the **CloudWatch Logs** console and find the log group for your Lambda function.
3. Verify that the file details (e.g., name and size) are logged.

