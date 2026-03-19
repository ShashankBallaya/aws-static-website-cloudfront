# AWS Static Website - S3 + CloudFront + HTTPS

>  A production-grade static website hosted on AWS using a private S3 bucket and CloudFront CDN with HTTPS enforcement. The S3 bucker is never publicly accessible - all traffic flows exclusively through CloudFront.

---

## Architecture 

![Architecture](architecture/project1-architecture.png)

```
User / Browser
	|
	|
	v
CloudFront Distribution
(CDN + HTTPS + Private S3 Access)
	|
	| CloudFront origin access (private)
	| AWS auto-manages S3 bucket policy 
	v
S3 Bucket (Private - Block all public access)
	|
	_ index.html
	_ error.html
```

**Key security principle:** The S3 bucket has all public access blocked. AWS automatically configures CloudFront with private bucker access - only the CloudFront distribution can read objects from S3. Accessing the S3 object URL directly returns `Access Denied`.

---

## Tech Stack

| Service | Purpose |
|---|---|
| AWS CloudFront | CDN - global content delivery + HTTPS enforcement |
| CloudFront Private S3 Access | Restricts S3 access to CloudFront only (replaces legacy OAC flow) |
| AWS CLI | All file uploads and syncs - no manual console uploads |

---

## How to Deploy 

Follow these steps exactly. All file uploads use the AWS CLI - not the console.

**Prerequisites**
- AWS account with IAM user configured.
- AWS CLI installed and configured (`aws configure`).
- draw.io or equivalent for architecture diagram.

**Step 1 - Create the HTML files**

Create `./site/index.html`:
```html
...

```

Create `./site/error.html`:
```html
...
```

