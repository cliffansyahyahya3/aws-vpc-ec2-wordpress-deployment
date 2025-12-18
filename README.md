
''' ROOT: AWS Cloud Infrastructure Deployment
│
├── 🔹 Networking (The Foundation)
│   ├── VPC: "YAHYA_VPC" (10.0.0.0/16)
│   │   ├── [Screenshot: vpc-configuration.png]
│   │   └── Role: Provides an isolated private network.
│   │
│   ├── Subnets (Traffic Isolation)
│   │   ├── Yahya Public Subnet 1 (10.0.1.0/24)
│   │   │   ├── [Screenshot: route-table-association.png]
│   │   │   └── Role: Hosts the web-facing WordPress instance.
│   │   └── YAHYA Private Subnet (10.0.2.0/24)
│   │       └── Role: Security layer for databases/internal resources.
│   │
│   └── Connectivity (The Gateway)
│       ├── Internet Gateway: "YAHYA_IG"
│       │   ├── [Screenshot: internet-gateway-setup.png]
│       │   └── Role: Allows the VPC to communicate with the internet.
│       └── Route Tables
│           └── Role: Maps the Public Subnet to the Internet Gateway.
│
├── 🔹 Compute (The Application)
│   ├── EC2 Instance: "WordPress" (t2.micro)
│   │   ├── [Screenshot: ec2-wordpress-instance.png]
│   │   ├── Region: us-west-1c (N. California)
│   │   └── Status: 2/2 Health Checks Passed
│   │
│   └── Networking Properties
│       ├── Public IPv4: 18.144.72.24
│       └── Private IP: 172.31.18.88
│
└── 🔹 Security (The Firewall)
    └── Security Groups
        ├── Inbound: Port 80 (HTTP) - Web Traffic
        └── Inbound: Port 22 (SSH) - Admin Access'''

Project Overview

This project demonstrates the manual configuration of a secure, production-ready cloud network on AWS. 
I moved beyond default settings to architect a Custom Virtual Private Cloud (VPC) with tiered subnets, 
ensuring high security and controlled traffic flow for a WordPress web server.

Skills & Technologies Demonstrated

  - Networking: VPC Design, Subnetting (CIDR), Route Tables, Internet Gateways (IGW).

  - Compute: EC2 Instance Provisioning (t2.micro).

  - Security: Security Group configuration and Network Isolation (Public vs. Private Subnets).

  - Cloud Administration: Monitoring resource health and status checks.

Network Architecture Breakdown
<img width="1920" height="947" alt="vpc-configuration" src="https://github.com/user-attachments/assets/1ec90046-cf0d-4c18-90cb-83b5796ceb1f" />

1. Virtual Private Cloud (VPC)

I designed a custom VPC named "YAHYA_VPC" with a 10.0.0.0/16 CIDR block to provide a private, isolated network environment.

  - VPC ID: vpc-0903d76a20b6a44e3

  - IPv4 CIDR: 10.0.0.0/16

2. Tiered Subnet Strategy
<img width="1920" height="947" alt="route-table-assosciation" src="https://github.com/user-attachments/assets/5e33f0e5-4b2d-46a1-b777-7710680b8c96" />

I implemented a tiered architecture to separate public-facing resources from private data:

  - Public Subnet: 10.0.1.0/24 — Hosted the WordPress web server with a route to the Internet Gateway.

  - Private Subnet: 10.0.2.0/24 — Reserved for database or internal resources to prevent direct exposure to the public internet.

3. Routing & Internet Access
<img width="1920" height="947" alt="internet-gateway-setup" src="https://github.com/user-attachments/assets/b3fc661e-7fee-4524-8059-d9ac65e40815" />

  - Internet Gateway (IGW): Created and attached YAHYA_IG to the VPC to enable internet communication.

  - Route Tables: Configured specific route table associations (rtb-01b683a...) to direct traffic from the Public Subnet to the Internet Gateway.

Compute Layer (WordPress Deployment)
<img width="1920" height="947" alt="ec2-wordpress-instance" src="https://github.com/user-attachments/assets/71f9e9d2-9105-4227-afe1-17a93d901648" />

Within the newly created network, I deployed a WordPress application on an EC2 instance.

  - Instance Type: t2.micro (Free Tier Eligible)

  - Availability Zone: us-west-1c

  - Status: Successfully passed 2/2 system health checks.

  - Accessibility: Accessible via Public IPv4 18.144.72.24.

Evidence of Deployment

All configurations were verified through the AWS Management Console.

  Custom VPC & Subnetting
  - Shows the creation of the isolated network environment.
  Internet Gateway Attachment
  - Proof of established internet connectivity for the public tier.
  Route Table Associations
  - Demonstrates the logic of mapping subnets to specific traffic routes.
  Final EC2 Instance State
  - The running WordPress server within the custom infrastructure.

What I learned

  - Security First: By utilizing a custom VPC instead of the default, I gained full control over the network's security posture.

  - Resource Isolation: I learned how to separate "Public" web tiers from "Private" data tiers using Route Tables.

  - Scalability: This foundation is ready for an Application Load Balancer (ALB) and Auto Scaling Groups to handle increased traffic.


