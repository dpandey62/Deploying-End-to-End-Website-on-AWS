# Deploying-End-to-End-Website-on-AWS


![Screenshot 2024-08-03 220815](https://github.com/user-attachments/assets/64adeb2b-6d9e-4372-94ea-415ac0f08720)
# Architecture Components
Route 53: Domain Name System (DNS) web service.

Amazon RDS: Relational Database Service.

S3: Simple Storage Service for static assets.

EC2: Elastic Compute Cloud for hosting the web server and application.


# Prerequisites
AWS Account with appropriate permissions.

Basic knowledge of AWS services.

A registered domain name (can be registered via Route 53).

# Step-by-Step Deployment
1. Register a Domain with Route 53

2. Login to AWS Console.

3.  Navigate to Route 53.

4.  Register a Domain:

Go to Domains > Registered Domains.
Click Register Domain.
Follow the instructions to register your domain.

#3. Set Up an S3 Bucket for Static Assets
Navigate to S3.

Create a Bucket:

Click Create bucket.

Enter a unique bucket name and choose the region.

Disable Block all public access.

Enable Static website hosting under the Properties tab.

Note the Bucket URL for later use.

Upload Your Static Files:

Upload your static website files (HTML, CSS, JS) to the bucket.

# 4. Set Up an RDS Instance
Navigate to Amazon RDS.

Create Database:

Click Create database.

Choose a database engine (e.g., MySQL, PostgreSQL).

Select Free tier if applicable.

Configure database settings (DB instance identifier, master username, password).

Choose VPC and Subnet settings.

Note the Endpoint and Port for later use.

Configure Security Group:

Ensure the security group allows incoming connections from your EC2 instance.

# 5. Set Up an EC2 Instance
Navigate to EC2.

Launch Instance:

Click Launch Instance.

Choose an Amazon Machine Image (AMI) (e.g., Amazon Linux 2).

Select an instance type (e.g., t2.micro for free tier).

Configure instance details, ensuring it is in the same VPC as your RDS instance.

Add storage as needed.

Configure security group:

Allow HTTP (port 80), HTTPS (port 443), and SSH (port 22) from your IP.

Launch the instance and download the key pair (.pem file).

Connect to Your EC2 Instance:

Use SSH to connect to your instance.

Example: ssh -i "your-key.pem" ec2-user@your-ec2-public-ip.

# 6. Install Web Server and Application

Install Web Server (e.g., Apache):

sudo yum update -y

sudo yum install httpd -y

sudo systemctl start httpd

sudo systemctl enable httpd

Deploy Your Application:

Copy your application files to /var/www/html.

Configure your application to connect to the RDS database using the endpoint and port.

# 7. Configure Route 53 for DNS
Create a Hosted Zone:

Navigate to Route 53.

Click Create hosted zone.

Enter your domain name.

Create Record Sets:

Add an A Record pointing to your EC2 instance's public IP.

Add a CNAME Record for your S3 bucket if hosting static assets separately.

# 8. Test Your Setup
Open Your Domain in a Browser:

Ensure it resolves to your EC2 instance and displays your website.

Verify that static assets are loading from S3.

Check database connections to RDS.

# Conclusion
By following these steps, you will have deployed an end-to-end website using AWS services. This setup ensures scalability, reliability, and ease of management. Make sure to monitor and optimize your AWS resources for cost efficiency and performance.




