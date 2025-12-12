# 🌐 Static Website Hosting on AWS (S3 + Route53 + CloudFront + ACM)

A complete guide to deploying a secure and scalable static website using **Amazon S3, CloudFront, Route53, and AWS Certificate Manager (ACM)**.

---

# 📝 Introduction  

Static website hosting is a simple, scalable, and cost-effective way to deploy front-end applications, portfolios, landing pages, or documentation sites.  
Using AWS services, we can make the website:

- 🚀 Fast (CDN powered by CloudFront)  
- 🔒 Secure (HTTPS using ACM SSL)  
- 🌍 Globally distributed  
- 💰 Low cost  
- 🎯 Highly available  

This project showcases how to deploy a static website with:

- **Amazon S3** – hosts static files  
- **AWS ACM** – SSL for HTTPS  
- **CloudFront** – CDN for fast delivery  
- **Route53** – DNS management  

---

# 🔧 Prerequisites  

Before starting, ensure you have the following:

---

## ✅ 1. AWS Account  
You need a valid AWS account with access to S3, CloudFront, ACM, and Route53.


## ✅ 2. A Registered Domain  
A domain name, preferably managed via AWS Route53.

Example used in this project:  
👉 `cloud-ops-studio.com`

<img width="1243" height="266" alt="image" src="https://github.com/user-attachments/assets/3ed7fd34-ac11-46ba-b146-cf6beabfb894" />


## ✅ 3. Static Website Files  
A project folder containing:
- index.html
- styles.css
- script.js


<img width="1033" height="149" alt="image" src="https://github.com/user-attachments/assets/f9f5293a-25e7-4303-b60e-9a9e4f048ec9" />



---

# 🚀 Step-by-Step Deployment Guide  

---

# 1️⃣ Create an S3 Bucket  

1. Open **Amazon S3**
2. Click **Create Bucket**
3. Bucket name = your domain  
   Example → `cloud-ops-studio.com`
4. Region: **us-east-1**
5. Disable **Block All Public Access**
6. Enable ACLs (if required)

<img width="1784" height="822" alt="image" src="https://github.com/user-attachments/assets/cd223f30-1a9f-4090-b920-9699db2e859a" />
 <br>
<img width="1721" height="514" alt="image" src="https://github.com/user-attachments/assets/90305e6b-c6a3-4503-908d-9d8545d6397f" />


---

# 2️⃣ Upload Website Files to S3  

- Go to your bucket → **Upload**
- Upload all files inside your website folder
- Include `index.html` at the root level

<img width="1683" height="447" alt="image" src="https://github.com/user-attachments/assets/6fa4c25e-d29b-47a0-b9c1-f0aa76f986ae" />


---

# 3️⃣ Enable Static Website Hosting in S3  

Navigate to:  
**Bucket → Properties → Static Website Hosting**

- Enable static website hosting  
- Set:
  - **Index document:** `index.html`  

S3 provides a website endpoint like:

http://cloud-ops-studio.com.s3-website-us-east-1.amazonaws.com


<img width="1718" height="682" alt="image" src="https://github.com/user-attachments/assets/216c4788-7ff5-48fe-b580-db6d47a62668" />


---

# 4️⃣ Request Free SSL Certificate in ACM (HTTPS)  

Go to:  
**AWS Certificate Manager → Request Certificate**

1. Choose **Request Public Certificate**
2. Add domain names:
   - `cloud-ops-studio.com`
   - `www.cloud-ops-studio.com`
3. Select **DNS Validation**
4. Copy the provided CNAME records to Route53

<img width="1593" height="192" alt="image" src="https://github.com/user-attachments/assets/a9548389-af80-4d3c-9580-640f8e850f89" />


---

# 5️⃣ Create a CloudFront Distribution  

Go to **CloudFront → Create Distribution**

---

### 🔹 Origin Settings  

| Setting | Value |
|--------|--------|
| Origin Domain | Your S3 website endpoint |
| Origin Access | Public or OAC |
| Viewer Protocol | Redirect HTTP → HTTPS |
| Allowed Methods | GET, HEAD |
| Default Root Object | `index.html` |

---

### 🔹 SSL Settings  

- Choose **Custom SSL Certificate**
- Select the ACM certificate you validated earlier

After creation, CloudFront provides a domain:

https://d123abcd1234.cloudfront.net


<img width="1632" height="614" alt="image" src="https://github.com/user-attachments/assets/80cd6bfd-30bd-486b-becf-cae558c0df04" />


---

# 6️⃣ Configure Route53 DNS Records  

Go to:  
**Route53 → Hosted Zones → cloud-ops-studio.com**

Create the following records ↓

---

### ✔ A Record (Alias → CloudFront Distribution)

| Name | Type | Alias | Target |
|------|-------|--------|--------|
| cloud-ops-studio.com | A | Yes | CloudFront URL |

---

### ✔ CNAME Record (Optional for www)

| Name | Type | Value |
|------|------|--------|
| www | CNAME | cloud-ops-studio.com |

<img width="601" height="330" alt="image" src="https://github.com/user-attachments/assets/94577409-6472-4804-8c6e-9d4e0986d61c" />


---

# 7️⃣ Test Your Website  

Visit:

👉 **https://cloud-ops-studio.com**

Check:
- 🔒 SSL (padlock icon)
- 🌍 Fast loading  
- 🚫 No AccessDenied  
- 📄 All files loading properly  

📌 *Screenshot:*  
`final-website.png`

---


# 🎯 Final Output  

Your entire static website is now:

✔ Secure (HTTPS)  
✔ Fast (CDN Caching)  
✔ Deployed with global coverage  
✔ Hosted on AWS  
✔ Served via custom domain  

---


# 🏁 Conclusion  

This project demonstrates a complete AWS deployment workflow for hosting a static website with enterprise-grade security and performance.  
You now have a **scalable, secure, and professional production-ready deployment architecture**.



