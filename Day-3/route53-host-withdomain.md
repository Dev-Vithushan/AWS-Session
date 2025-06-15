### ✅ Prerequisites:

* An S3 bucket with your static website (e.g., `index.html`)
* A registered domain (e.g., `example.com`) — can be via Route 53 or external
* (Optional) You have a certificate if using HTTPS with CloudFront (explained below)

---

## 🚀 Step-by-Step Configuration:

---

### **1. Create and Configure the S3 Bucket**

#### 🔹 Create the bucket:

* Name your bucket **exactly** like your domain (e.g., `example.com` or `www.example.com`)
* Uncheck **Block all public access**
* Enable **static website hosting** under bucket > Properties:

  * Select “Use this bucket to host a website”
  * Index document: `index.html`
  * (Optional) Error document: `error.html`

#### 🔹 Make files publicly accessible:

* Add a bucket policy like:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example.com/*"
    }
  ]
}
```

---

### **2. Set Up Route 53 Hosted Zone**

* Go to **Route 53 > Hosted Zones**
* Click **Create Hosted Zone**

  * Domain Name: `example.com`
  * Type: Public Hosted Zone

---

### **3. Add DNS Records**

#### 🔹 Add an **A Record** (alias to S3 website):

* In your hosted zone:

  * Click **Create record**
  * Record name: leave blank (for root domain) or enter `www`
  * Record type: **A – IPv4 address**
  * Choose **Alias: Yes**

    * Route traffic to → **Alias to S3 website endpoint**
    * Select the correct region and bucket endpoint from dropdown

> Note: S3 website hosting **only supports HTTP**. If you want **HTTPS**, use **CloudFront** (optional below).

---

### **4. Point Domain to Route 53 (if domain is external)**

If domain is from **GoDaddy, Namecheap**, etc.:

* Go to your domain registrar
* Update the **Nameservers (NS)** to those given by Route 53 under **Hosted Zone > NS record**

---

### ✅ (Optional) Enable HTTPS with CloudFront + ACM

* Create an **SSL certificate** in **ACM** (Amazon Certificate Manager)
* Create a **CloudFront distribution**:

  * Origin domain: your **S3 website endpoint**
  * Set viewer protocol policy to **Redirect HTTP to HTTPS**
  * Attach the ACM certificate
* In Route 53:

  * Set an **A Record** → **Alias to CloudFront distribution**

---


* Within a few minutes (or up to 30), visiting `https://www.example.com` or `http://example.com` should load your static site from S3.

