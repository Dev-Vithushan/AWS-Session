### **Hosting a Static Website on AWS S3**  

This is a simple yet powerful hands-on task to showcase how to host a static website using an Amazon S3 bucket.

---

#### **Steps to Host a Static Website on S3**  

---

### **Task Objective**
Host a static website using an S3 bucket and configure public access.

---

### **Hands-On Steps**

#### **Step 1: Create an S3 Bucket**
1. Go to the **AWS Management Console** and navigate to **S3**.
2. Click **Create Bucket** and provide:
   - A globally unique bucket name (e.g., `my-static-website-demo`).
   - Choose a Region close to your location.
3. Uncheck the **Block all public access** box (for public hosting) and acknowledge the warning.

---

#### **Step 2: Enable Static Website Hosting**
1. Open the newly created bucket and go to the **Properties** tab.
2. Scroll to the **Static website hosting** section and:
   - Enable it.
   - Specify the **Index document** (e.g., `index.html`).
   - Optionally, specify an **Error document** (e.g., `error.html`).
3. Save the settings.

---

#### **Step 3: Upload Website Files**
1. Prepare your website files (e.g., `index.html` and `error.html`).
2. Click the **Upload** button in the S3 bucket and add your files.
3. After uploading, go to the **Permissions** tab and:
   - Select the uploaded objects.
   - Make them **public** using the Object actions menu.

---

#### **Step 4: Add a Bucket Policy for Public Access**
1. Go to the **Permissions** tab and click on **Bucket policy**.
2. Add the following bucket policy to allow public read access:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::my-static-website-demo/*"
           }
       ]
   }
   ```
   Replace `my-static-website-demo` with your bucket name.

---

#### **Step 5: Access the Website**
1. Go back to the **Properties** tab and find the **Static website hosting** section.
2. Copy the **Bucket website endpoint** URL.
3. Open the URL in a browser to view your static website.

