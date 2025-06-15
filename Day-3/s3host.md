Here’s a **step-by-step procedure** to deploy a **static website on an Amazon S3 bucket**:

---

### ✅ **Step 1: Create an S3 Bucket**

1. **Go to the AWS Console** → Navigate to **S3** service.
2. Click **“Create bucket”**.
3. **Bucket Name**: Enter a globally unique name (e.g., `my-static-site-vithushan`).
4. **Region**: Choose a region (e.g., Asia Pacific (Mumbai) `ap-south-1`).
5. **Uncheck "Block all public access"** under permissions (important for website access).
6. Acknowledge the warning → Click **Create bucket**.

---

### ✅ **Step 2: Upload Your Website Files**

1. Click on the created bucket name.
2. Go to the **Objects** tab → Click **Upload**.
3. **Add Files** → Upload your `index.html`, `style.css`, `script.js`, etc.
4. Click **Upload**.

---

### ✅ **Step 3: Enable Static Website Hosting**

1. Go to the **Properties** tab of the bucket.
2. Scroll down to **Static website hosting**.
3. Click **Edit**.
4. Choose **Enable**.
5. **Index document**: `index.html`
6. (Optional) **Error document**: `error.html`
7. Click **Save changes**.

---

### ✅ **Step 4: Set Bucket Policy to Make Website Public**

1. Go to the **Permissions** tab.
2. Click on **Bucket policy**.
3. Add the following JSON (replace `your-bucket-name`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForStaticWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

4. Click **Save**.

---

### ✅ **Step 5: Access Your Static Website**

1. Go back to the **Properties** tab.
2. Scroll to **Static website hosting** → You will see a **Website endpoint**.
3. Open that URL in a browser → You should see your static site live 🎉

---
