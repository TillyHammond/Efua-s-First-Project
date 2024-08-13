Static Website Deployment on EC2 using Nginx
Introduction
This documentation covers the steps to deploy a static website on an Amazon EC2 instance running Ubuntu with Nginx as the web server. The static website files are hosted on the instance and served to the public via Nginx.

Prerequisites
Amazon EC2 Instance:

An EC2 instance running Ubuntu.
SSH access to the instance.
Nginx Web Server:

Installed and configured on the EC2 instance.
Static Website Files:

HTML, CSS, JavaScript.

*Steps*
1. Connect to Your EC2 Instance
Use SSH to connect to your EC2 instance:
sh
Copy the following code to your project IDE
ssh -i /path/to/your-key.pem ubuntu@your-ec2-public-ip

2. *Update the System*
Update the package lists to ensure you have the latest information:
sh
Copy code
sudo apt update
sudo apt upgrade -y


3. *Install Nginx*
If Nginx is not already installed, you can install it using:

sh
Copy the following packages List into your IDE and run the following command
sudo apt install nginx -y
Start and enable Nginx to run on boot:

sh
Copy the following packages List into your IDE and run the following command
sudo systemctl start nginx
sudo systemctl enable nginx


4. *Upload Your Static Website Files*
Copy your static website files to the /var/www/html directory on the server:

sh
Copy the following package
sudo cp -r /path/to/your/website/* /var/www/html/
Ensure the files are accessible by adjusting permissions if necessary:

sh
Copy the following package
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html


5. *Configure Nginx*
If needed, you can configure Nginx by editing the default site configuration file:

sh
Copy the following configuration
sudo nano /etc/nginx/sites-available/default
Ensure the server block is configured to serve the website:

nginx
Copy the following configuration
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.html;

    server_name your-domain.com www.your-domain.com;

    location / {
        try_files $uri $uri/ =404;
    }
}
Save and close the file (in Nano, press CTRL + X, then Y, and ENTER).


6. *Test Nginx Configuration*
Test the Nginx configuration to ensure there are no syntax errors:

sh
Copy the configuration
sudo nginx -t
If the test is successful, reload Nginx to apply the changes:

sh
Copy the configuration 
sudo systemctl reload nginx


7. *Access Your Website*
Your static website should now be accessible from your EC2 instance's public IP or domain name (if configured). Open a web browser and visit:
vbnet
Copy the configuration
http://your-ec2-public-ip
or
arduino
Copy the configuration
http://your-domain.com


8. *Security Groups and Firewall*
Ensure your EC2 instance's security groups allow HTTP (port 80) traffic:
In the AWS Management Console, navigate to EC2 > Security Groups.
Edit the security group associated with your instance to allow inbound HTTP traffic on port 80.


9. *Troubleshooting*
Check Nginx Status: Ensure Nginx is running:

sh
Copy the following
sudo systemctl status nginx
View Nginx Logs: Check the Nginx error logs for any issues:

sh
Copy the following
sudo tail -f /var/log/nginx/error.log


*Conclusion*
Your static website is now successfully deployed on an EC2 instance using Nginx. It is accessible via the instance's public IP or your domain name. You can further enhance your setup by configuring SSL using Let's Encrypt or setting up a custom domain.


