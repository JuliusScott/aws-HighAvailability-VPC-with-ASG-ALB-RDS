# AWS High Availability VPC with ALB, Auto Scaling Group, Amazon RDS, and Systems Manager

## 1. Create the VPC

- Create the VPC
- Define the CIDR block

---

## 2. Create Subnets

### Public Subnets
- Create Public Subnet 1
- Create Public Subnet 2

### Private Application Subnets
- Create Private App Subnet 1
- Create Private App Subnet 2

### Private Database Subnets
- Create Private DB Subnet 1
- Create Private DB Subnet 2

---

## 3. Make Public Subnets Public

### Configure Public Subnets
- Enable Auto-Assign Public IPv4 Addresses

### Internet Gateway
- Create Internet Gateway (IGW)
- Attach IGW to the VPC

### Public Route Table
- Create Public Route Table
- Create Route:
  - `0.0.0.0/0 → Internet Gateway`
- Associate Public Subnet 1
- Associate Public Subnet 2

---

## 4. Create NAT Gateway

### NAT Gateway
- Allocate Elastic IP Address
- Create NAT Gateway

### Private Route Table
- Create Private Route Table
- Create Route:
  - `0.0.0.0/0 → NAT Gateway`
- Associate Private App Subnets

---

## 5. Create Security Groups

### Application Load Balancer Security Group
- ALB Security Group

### Application Security Group
- EC2 Application Security Group

### Database Security Group
- Amazon RDS Security Group

### Systems Manager Security Group
- VPC Endpoint Security Group

---

## 6. Create IAM Trust Policy and Role

### IAM Trust Policy
- Create Trust Policy JSON File

### IAM Role
- Create IAM Role for EC2

### IAM Policies
- Attach Required IAM Policies

### Instance Profile
- Create Instance Profile
- Add Role to Instance Profile

### Launch Configuration
- Attach Instance Profile During EC2 Launch

---

## 7. Create VPC Endpoints for Private EC2 Access

### Systems Manager Endpoints
- Systems Manager (SSM)
- Systems Manager Messages (SSMMessages)
- EC2 Messages (EC2Messages)

---

## 8. Create the Application Load Balancer

### Load Balancer Configuration
- Create Application Load Balancer
- Place ALB in Public Subnet 1
- Place ALB in Public Subnet 2
- Attach ALB Security Group

---

## 9. Create Target Group and Listener

### Target Group
- Create Target Group
- Configure Health Checks

### Listener
- Create HTTP Listener
- Forward Traffic to Target Group

---

## 10. Launch EC2 Instances

### EC2 Configuration
- Launch EC2 Instances in Private App Subnets
- Attach EC2 Security Group
- Attach SSM IAM Role

### Install Application Components
- Install Web Server
- Start Web Server Service

---

## 11. Register EC2 Instances with Target Group

- Register EC2 Instances
- Verify Target Registration

---

## 12. Validate ALB to EC2 Connectivity

### Health Checks
- Confirm Targets Become Healthy

### Application Test
- Access ALB DNS Name
- Verify Web Page Loads Successfully

---

## 13. Create RDS Subnet Group

### Database Subnets
- Create RDS Subnet Group
- Include Both Private DB Subnets

---

## 14. Create Amazon RDS Database

### Database Configuration
- Engine:
  - MySQL **or**
  - PostgreSQL
- Private Access Only
- Single-AZ Deployment (Lab Environment)

---

## 15. Allow EC2 to RDS Communication

### Database Security Group
- Allow Database Port from EC2 Security Group Only

#### Example Ports
- MySQL: `3306`
- PostgreSQL: `5432`

---

## 16. Create Launch Template

### Launch Template
- Create `launch-template.json`
- Create Launch Template from JSON File

---

## 17. Create Auto Scaling Group

### Auto Scaling Configuration
- Define Minimum Capacity
- Define Maximum Capacity
- Define Desired Capacity

### Load Balancer Integration
- Attach Target Group ARN

---

## 18. Validate EC2 to RDS Connectivity

### Database Connection Test
- Connect from EC2 Using Database Client

### Database Validation
- Create Database
- Create Table
- Insert Test Data
- Run Test Query

---

# Final Architecture Validation

Validate the following:

- ALB Targets Healthy
- Auto Scaling Group Healthy
- EC2 Instances Healthy
- Session Manager Access Working
- Database Connectivity Working
- Application Accessible Through ALB DNS Name

## Architecture Flow

```text
Internet
    │
    ▼
Application Load Balancer (Public Subnets)
    │
    ▼
EC2 Instances (Private App Subnets)
    │
    ▼
Amazon RDS (Private DB Subnets)
```

**Result:**

> Internet → ALB → Private EC2 → Private RDS
>
> Highly Available Web Application Architecture with Systems Manager Access and Auto Scaling.
