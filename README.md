# Ghackk-Technologies

Step 1: Set Up Your AWS Environment
    1. Sign In to AWS Console:

        Go to the AWS Management Console.
        Sign in with your AWS account.

    2. Create an EC2 Instance:
        Navigate to EC2 in the AWS Console.
        Click on Launch Instance.
        Choose an Amazon Machine Image (AMI), like Amazon Linux 2.
        Select an instance type (e.g., t2.micro for free tier).
        Configure instance details as needed and click Next.
        Add storage (default is usually sufficient).

    3. Configure Security Group:
        Add rules for HTTP (port 80) and SSH (port 22).
        Click Launch, select or create a key pair, and launch your instance.

    4. Connect to Your EC2 Instance:
        Open your terminal (or Command Prompt) and use SSH to connect
        ssh -i "your-key-pair.pem" ec2-user@your-ec2-public-dns

Step 2: Set Up Your Web Application
    1. Install Necessary Packages:
        sudo yum update -y
        sudo yum install nginx -y
        sudo systemctl start nginx
        sudo systemctl enable nginx
        cd /usr/share/nginx/html
        sudo rm index.html
        sudo nano index.html

Step 3: Configure S3 for Image Storage (Optional)
    1. Create an S3 Bucket:
        Navigate to S3 in the AWS Console.
        Click Create Bucket.
        Enter a unique bucket name and choose the region.
        Configure settings as needed and create the bucket.
    2. Upload Images:
        Click on the bucket name and then click Upload to add images.

Step 4: Set Up a Database

    1.Create an RDS Database:
        Navigate to RDS in the AWS Console.
        Click Create database.
        Choose MySQL and select the free tier option.
        Configure the database settings (DB name, master username, password).
        Select a VPC and subnets (default options are usually sufficient).
        Configure Security Groups to allow access (add rules for the EC2 instance).
    2. Connect to Your RDS Database:
        Use the following commands to connect to your RDS instance from your EC2 instance
        sudo yum install mysql -y
        mysql -h your-rds-endpoint -u your-master-username -p

            CREATE TABLE manhwa (
            id INT AUTO_INCREMENT PRIMARY KEY,
            title VARCHAR(255) NOT NULL,
            genre VARCHAR(100),
            description TEXT
            );

Step 6: Enable HTTPS

    1. Request an SSL Certificate:
        Go to Certificate Manager and click on Request a Certificate.
        Enter your domain or public DNS name.

    2. Configure Nginx for SSL:
        Install Certbot for SSL certificate management
        sudo yum install certbot python2-certbot-nginx -y
        sudo certbot --nginx

    server {
        listen 80;
        server_name your-public-dns;

        return 301 https://$host$request_uri;
    }

    sudo systemctl restart nginx

