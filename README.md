# Project---HADR-High-Availability-And-Disaster-Recover
Step 1:
·       Launch a template in the Mumbai region.
·       Instance Type: t2.micro
·       Selected Amazon Linux 2023 kernel-6.1 AMI
·       Security Group: Allow SSH (22), HTTP (80), and HTTPS (443) (for testing purposes).
·       User data:
#!/bin/bash
sudo su -
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "Hello from Mumbai Region" > /var/www/html/index.html
Step 2:
 
·       Create an Auto Scaling group with the same template.
·       With Desire capacity 1; min-max 1-2
Step 3:
·       Create target group attach autoscaling group
·       Create Application Load Balancer (ALB)
·       Listener http(80) forward to target group
Repeating same steps in N.Virginia region  with only change in user data
echo "Hello from N.Virginia Region" > /var/www/html/index.html
 
Step 4
·       Now configure route 53 with failover policy
·       Create a new hosted zone
·       Add 2 A-records
Record 1 : Primary  Alias (For Mumbai region)
Record 2: Secondary (For N.Virginia region)
·       Add record id for different hosted zone regions
Results: Now when we access the through our Domain, it  transfers the traffic to  Mumbai region. As it is our primary region. If any unfortunate event happens and the server becomes unhealthy. It automatically transfers traffic to the secondary region. i.e., N. Virginia region—this ensures disaster recovery. And meanwhile auto scaling group terminate unhealthy server and create new server this ensure availability.
 


<img width="1890" height="867" alt="2-13" src="https://github.com/user-attachments/assets/8e4c4f2a-acfe-47e7-b6d0-6073c2257927" />
<img width="1951" height="919" alt="2-01" src="https://github.com/user-attachments/assets/d40db95f-382f-46d5-8c70-b40aa4b31456" />
<img width="1920" height="884" alt="2-02" src="https://github.com/user-attachments/assets/dddb1a8e-c535-4a3d-bb33-0eeecb2967ff" />
<img width="1920" height="920" alt="2-03" src="https://github.com/user-attachments/assets/204e2fae-000c-42a6-8c84-dc4f0ac6930b" />
<img width="1910" height="894" alt="2-3" src="https://github.com/user-attachments/assets/6aee9719-861a-42f5-8eaf-fc2e61ae5070" />
<img width="1911" height="881" alt="2-5" src="https://github.com/user-attachments/assets/0137cee3-8ff7-4ffd-b15d-1b9a0b423d26" />
<img width="1920" height="892" alt="2-4" src="https://github.com/user-attachments/assets/506c38c2-6b66-44de-94dd-b7257b29c13d" />
<img width="1920" height="922" alt="2-14" src="https://github.com/user-attachments/assets/f3a99f1d-480b-4f7d-a04d-4e1f57c071c9" />
<img width="1920" height="898" alt="2-8" src="https://github.com/user-attachments/assets/69a2ffa8-ac5d-468e-824e-afad54d638b3" />
<img width="1914" height="884" alt="2-9" src="https://github.com/user-attachments/assets/89b948fd-1a5c-46dd-9393-197f8809ae3e" />
<img width="1920" height="934" alt="2-10" src="https://github.com/user-attachments/assets/307cab1f-cd6f-4cdd-aed0-36fb08641698" />
<img width="1920" height="890" alt="2-11" src="https://github.com/user-attachments/assets/6f5d08cf-6f75-4573-8969-3ebce8684126" />
<img width="1920" height="922" alt="2-12" src="https://github.com/user-attachments/assets/b4590007-66b8-478b-9921-8a1e1d37f442" />
<img width="1908" height="875" alt="2-7" src="https://github.com/user-attachments/assets/8f0c7a03-b13b-4a18-8659-92025dab30d4" />
<img width="1918" height="699" alt="2-1" src="https://github.com/user-attachments/assets/2fe8ed4f-fdfd-453a-9a12-9ab6e512d821" />
<img width="1920" height="693" alt="2-2" src="https://github.com/user-attachments/assets/9c146c79-8f41-4c3b-b929-b07a2c29de79" />













