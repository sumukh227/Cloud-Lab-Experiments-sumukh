# AWS Cloud Computing Experiments

## Experiment 3: Launching an Amazon EC2 Instance

### Steps
1. Log in to the AWS Management Console.
2. Search for EC2 and open the EC2 dashboard.
3. Select the preferred AWS Region (e.g., Asia Pacific (Mumbai) or US East (N. Virginia)).
4. Click Launch instance.
5. Under Name and tags, enter a name (e.g., My-Ubuntu-Server).
6. Under Application and OS Images (AMI), select Ubuntu and ensure Free tier eligible is selected.
7. Under Instance type, select t2.micro (or t3.micro).
8. Under Key pair, click Create new key pair, choose RSA and .pem format, and download the key file.
9. Under Network settings, allow SSH traffic from My IP and optionally check Allow HTTP traffic.
10. Leave default storage settings and click Launch instance.
11. Click View all instances and verify the instance state changes from Pending to Running.

---

## Experiment 8: Deploying a Web Application on Amazon EC2

### Steps
1. Open the EC2 dashboard and click Launch instance.
2. Under Name and tags, enter web-server.
3. Select Amazon Linux under Application and OS Images (AMI).
4. Under Instance type, select t3.micro.
5. Create and download a new key pair (.pem format).
6. Under Network settings, allow SSH, HTTP, and HTTPS traffic.
7. Keep default storage and launch the instance.
8. Go to Instances, select web-server, click Connect, and choose EC2 Instance Connect.
9. Switch to root user:
sudo su -
10. Update system packages:
yum update -y
11. Install Apache HTTP server:
yum install -y httpd
12. Navigate to web directory:
cd /var/www/html
13. Create index file:
nano index.html
14. Add HTML code:
<!DOCTYPE html>
<html>
<head>
    <title>My EC2 Web Application</title>
</head>
<body>
    <h1>Hello from AWS EC2!</h1>
    <p>This web page is deployed on an EC2 instance.</p>
    <p>Cloud Computing Lab</p>
</body>
</html>
15. Save and exit (Ctrl + O, Enter, Ctrl + X).
16. Enable and start Apache server:
systemctl enable httpd
systemctl start httpd
17. Verify service status:
systemctl status httpd
18. Copy the Public IPv4 address of the EC2 instance and open it in a browser to view the webpage.

---

## Experiment 10: Hosting a Static Web Application on Amazon S3

### Steps
1. Open the S3 dashboard and click Create bucket.
2. Enter a unique bucket name and choose the AWS Region.
3. Uncheck Block all public access and acknowledge the warning.
4. Keep other settings default and click Create bucket.
5. Open the created bucket, go to the Properties tab, and scroll to Static website hosting.
6. Click Edit, select Enable, set hosting type to Host a static website, set index document to index.html, and save changes.
7. Note down the Bucket website endpoint URL.
8. Go to the Permissions tab, click Edit under Bucket policy, and paste the read policy:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
9. Replace YOUR_BUCKET_NAME with the actual bucket name and save changes.
10. Create index.html locally with sample code:
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Static Website</title>
</head>
<body>
    <h1>Welcome to My AWS Website</h1>
    <p>This website is hosted using Amazon S3.</p>
    <p>Static Web Application</p>
</body>
</html>
11. Go to the Objects tab in S3, click Upload, add index.html, and confirm upload.
12. Open the Bucket website endpoint in a web browser to verify the hosted site.

---

## Experiment 11: Content Delivery and Media Streaming using Amazon CloudFront

### Steps
1. Open the S3 dashboard and click Create bucket.
2. Enter a unique bucket name and select the region.
3. Keep Block all public access enabled and leave SSE-S3 encryption enabled.
4. Click Create bucket.
5. Open the bucket, click Upload, select a media (.mp4) file, and upload it.
6. Search for CloudFront in AWS Console and click Create distribution.
7. Under Origin domain, select the S3 bucket created.
8. Under Origin access, select Origin access control settings (OAC) and create control setting with default values.
9. Under Default cache behavior, set Viewer protocol policy to Redirect HTTP to HTTPS.
10. Set Allowed HTTP methods to GET, HEAD and Cache policy to CachingOptimized.
11. Under Web Application Firewall (WAF), select Do not enable security protections.
12. Click Create distribution and wait for the deployment to finish.
13. Copy the CloudFront generated policy and update the S3 bucket policy to allow OAC access.
14. Copy the CloudFront Distribution Domain Name, append the media filename (e.g., https://DISTRIBUTION_DOMAIN/video.mp4), and open it in a browser to test streaming.