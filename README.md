# AWS 8-Week Roadmap – Final Project

This repository documents my journey through an **8-week AWS Cloud Engineering Roadmap**.  
It includes Infrastructure-as-Code (CloudFormation templates), test evidence (screenshots), and supporting documentation.

The final project demonstrates a production-style architecture with **VPC, Bastion Host, Application Load Balancer (ALB), Auto Scaling Group (ASG), RDS MySQL Database, and CloudWatch Monitoring**.

---

## Repository Structure

aws-8-week-roadmap/
│
├── final-project-template.yaml      # Final production CloudFormation template
│
├── other_templates/                 # Earlier Week 7–8 templates
│   ├── week7-day1.yaml
│   ├── week7-day2.yaml
│   ├── week7-day3.yaml
│   ├── week7-day4.yaml
│   ├── week7-day5.yaml
│   └── week8-day2.yaml
│
├── screenshots/                     # Blurred AWS Console + CLI screenshots
│
├── 8-Week AWS Roadmap Overview.pdf  # First book: Roadmap documentation
├── Cloud-Engineer-Playbook.pdf      # Second book: Broader handbook (to be added soon)
│
└── README.md

---

## Final Architecture Features

- **Networking**
  - Custom VPC with public + private subnets in multiple AZs
  - NAT Gateway for secure outbound access
  - Route tables configured for IGW + NAT

- **Security**
  - Security Groups for Bastion, ALB, Web ASG, and Database
  - SSH access restricted to Bastion host only

- **Compute**
  - Auto Scaling Group (ASG) across private subnets
  - Launch Template installs nginx with instance ID + AZ in index page

- **Database**
  - RDS MySQL instance in private subnets
  - Not publicly accessible

- **Monitoring**
  - CloudWatch CPU alarm with SNS email subscription
  - Alarm test performed with threshold temporarily lowered to 20% (note for reviewers)

---

## Tests and Evidence

All screenshots in `screenshots/` demonstrate successful tests:

1. VPC + Subnet Layout – custom CIDR and subnet mapping  
2. Auto Scaling Group – two instances distributed across AZs  
3. ALB DNS endpoint – curl shows responses from different instances  
4. Bastion SSH – secure access into private subnet web servers  
5. RDS Database – private endpoint reachable only from web tier  
6. CloudWatch Alarm – email notification received on CPU threshold breach  
7. Security Groups – Bastion, Web, ALB, DB with least privilege rules  
8. Tags – consistent tagging across resources  

---

## Documentation

- **8-Week AWS Roadmap Overview (PDF):** Step-by-step record of each week’s progress.  
- **The Cloud Engineer’s Playbook (PDF):** Broader handbook (“From Zero to Deployed”), covering concepts, tools, and soft skills. *(Final version coming soon.)*

---

## Usage

To deploy a template:

```bash
aws cloudformation create-stack \
  --stack-name test-stack \
  --template-body file://final-project-template.yaml \
  --capabilities CAPABILITY_IAM
```
Outputs include:

ALB DNS – web entry point

Bastion IP – SSH access

DB Endpoint – internal MySQL address

## Author

#### Khalid Suliman
MEng Electronic & Software Engineering – University of Aberdeen

Notes

All sensitive details (IPs, ARNs, account IDs) are blurred in screenshots.

Templates and configs are for educational/demo purposes, not production.
