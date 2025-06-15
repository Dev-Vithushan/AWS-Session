

## 🚀 Step-by-Step: Deploy React App to S3

---

### ✅ Prerequisites:

* AWS account
* AWS CLI installed & configured (`aws configure`)
* A React app created using `create-react-app`

---

### **1. Build the React App**

In your project folder:

```bash
npm run build
```

This creates a production-ready static site in the `/build` directory.

---

### **2. Create an S3 Bucket**

You can do this via AWS Console or CLI. Bucket name should match your domain (if using one).

#### Option A: **Via Console**

* Go to **S3 → Create Bucket**
* Name it (e.g., `my-react-app`)
* **Uncheck** "Block all public access"
* Enable **Static website hosting** in **Properties**

  * Index document: `index.html`
  * Error document: `index.html` (for React Router)

#### Option B: **Via CLI**

```bash
aws s3 mb s3://my-react-app
aws s3 website s3://my-react-app/ --index-document index.html --error-document index.html
```

---

### **3. Set Public Read Policy**

Go to **Permissions > Bucket Policy**, and add:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-react-app/*"
    }
  ]
}
```

---

### **4. Upload Build Files**

#### Option A: **Via Console**

* Open your S3 bucket
* Upload **all files** inside the `/build` folder (not the folder itself)

#### Option B: **Via CLI**

```bash
aws s3 sync build/ s3://my-react-app --delete
```

---

### **5. Access Your Website**

* Go to **Bucket → Properties → Static website hosting**
* Copy the **endpoint URL** (e.g., `http://my-react-app.s3-website-us-east-1.amazonaws.com`)
* Visit in browser — your React app should load!

---

## ⚠️ Optional: Use a Custom Domain + HTTPS

* Use **Route 53** + **CloudFront** + **ACM** for:

  * Domain mapping (e.g., `www.example.com`)
  * HTTPS support

