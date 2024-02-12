# Hosting a Static Website on AWS

This project aimed to deploy a static HTML web application on Amazon Web Services (AWS) utilizing various resources and configurations. Below is an overview of the setup and deployment process.

## Configuration Overview

1. **Virtual Private Cloud (VPC):** Configured with public and private subnets across two availability zones for enhanced fault tolerance.

2. **Internet Gateway:** Deployed to facilitate connectivity between VPC instances and the wider Internet.

3. **Security Groups:** Implemented as a network firewall mechanism to control inbound and outbound traffic.

4. **Availability Zones:** Utilized two availability zones to enhance system reliability.

5. **Subnet Utilization:** Public subnets utilized for infrastructure components like NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint:** Implemented for secure connections to assets within both public and private subnets.

7. **Web Server Positioning:** Web servers (EC2 instances) positioned within private subnets for enhanced security.

8. **NAT Gateway:** Enabled instances in private subnets to access the Internet.

9. **Website Hosting:** Hosted the website on EC2 instances.

10. **Application Load Balancer (ALB):** Employed for evenly distributing web traffic to an Auto Scaling Group of EC2 instances across multiple availability zones.

11. **Auto Scaling Group:** Managed EC2 instances automatically to ensure website availability, scalability, fault tolerance, and elasticity.

12. **Version Control:** Web files stored on GitHub for version control and collaboration.

13. **Certificate Manager:** Secured application communications using SSL certificates.

14. **Simple Notification Service (SNS):** Configured to alert about activities within the Auto Scaling Group.

15. **Route 53:** Registered the domain name and set up a DNS record for the website.

## Deployment Script

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/KAbiJordan/Host-a-static-website-on-AWS.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-static-website-on-AWS/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-static-website-on-AWS
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

This script automates the setup process by updating packages, installing Apache HTTP Server, cloning the project repository from GitHub, copying files to the web root, enabling and starting the server.

## Conclusion

By following these configurations and utilizing the deployment script, the static website was successfully hosted on AWS, ensuring reliability, security, and scalability.
