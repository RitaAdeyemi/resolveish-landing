ResolveISH Landing Page Deployment

 Project Overview
This project showcases a deployed landing page for ResolveISH, a web application solution focused on helping users in Nigeria resolve interbank transaction issues. HTML with embedded CSS animations, and it was deployed on an Apache web server running on an Ubuntu EC2 instance.


 Server Setup

- Cloud Provider: AWS EC2
- Instance Type: t3.micro (Free Tier, eu-north-1 region)
- AMI: Ubuntu Server 24.04 LTS
- Key Pair: Created TestKey.pem and downloaded it to access the instance via SSH
- Security Group: 
  - Allowed Port 22 (SSH) in my EC2 Security group
  - Allowed Port 80 (HTTP) in EC2 Security group
  - Allowed Port 443 (HTTPS) in EC2 Security group


  Web Server Installation

- Installed Apache2 using:
  sudo apt update
  sudo apt install apache2 -y
- Confirmed Apache2 was running by visiting my public IP address http://51.21.190.29 in a browser and saw the Apache2 Ubuntu default page


## Deployment Steps
1. Created Landing Page
   - Built a customized index.html landing page with embedded CSS and basic animations in VS Code.
   - Saved the file inside a folder named ALTSCHOOL PROJECT on my desktop
2. Prepared SSH Access
   - Connected to the EC2 instance using SSH:ssh -i ~/Downloads/TestKey.pem ubuntu@51.21.190.29
   - After I had run: chmod 400 Testkey.pem 
   - That gave appropriate permission to the key file
3. Uploaded my index.html file to the server using SCP and escaped space in the folder name by including \ :
 scp -i ~/Downloads/TestKey.pem ~/Desktop/ALTSCHOOL\ PROJECT/index.html ubuntu@51.21.190.29:/home/ubuntu
4. Moved the index.html file to Apache first verifying the file exists and upload it using
   - ls /home/ubuntu/index.html
   - Then I moved same file from /home/ubuntu/ into Apache’s root directory:
   sudo mv index.html /var/www/html/
5. Opened my browser and entered my EC2 public DNS:ec2-51-21-190-29.eu-north-1.compute.amazonaws.com to see my personalized landing page for ResolveISH
6.  I opened port 443 in my EC2 instance security group to allow HTTPS traffic access
- Tested the site by opening https://51.21.190.29 in my browser(Ignore browser warning because this is a self-signed cert)

7. SSL Certificate(was optional)
This project was not secured with SSL due to the absence of a custom domain. If a custom domain is used in the future, SSL can be enabled using:
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
Let's Encrypt SSL via Certbot requires a Fully Qualified Domain Name and cannot issue a certificate to a raw IP address.

Access the live landing page here:
 (https://51.21.190.29)

Note: This IP may not show a padlock icon (https) because SSL was not applied. The page is still publicly accessible and functional.

Preview of the page:

<img width="1359" alt="Screenshot" src="https://github.com/user-attachments/assets/98332c5e-6ba8-4bd4-a3dc-633333d0abba" />


Repository Content:
- index.html: The deployed landing page
- README.md – Deployment steps and documentation
- screenshot.png - visual preview of the page
  
Acknowledgement:
This project's created as part of the ALTSchool Africa Cloud Engineering program for 2nd Semester.
