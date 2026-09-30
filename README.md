# AWS Cloud Application

A hands-on cloud application project developed and deployed on **Amazon Web Services (AWS)** to understand cloud infrastructure, application deployment, networking, load balancing, and database integration.

## Project Overview

The application was deployed on AWS using separate components for the web interface, backend application, and database.

The project demonstrates how a user request can travel through the AWS infrastructure from the frontend to the backend application and finally to the database.

## Architecture

```text
                    User
                      |
                      v
              React Web Application
                      |
                      v
                   Nginx
                 Web Tier
                  EC2
                      |
                      v
        Internal Application Load Balancer
                      |
                      v
             Node.js / Express
              Application Tier
                 EC2
               Port 4000
                      |
                      v
             Amazon RDS MySQL
                  Database
```

## Application Flow

```text
User
  ↓
React Frontend
  ↓
Nginx
  ↓
Internal Application Load Balancer
  ↓
Node.js / Express Backend
  ↓
Amazon RDS MySQL
  ↓
Response returned to the user
```

## AWS Services Used

* **Amazon EC2** – Application and web server hosting
* **Amazon RDS MySQL** – Relational database
* **Application Load Balancer** – Internal traffic distribution
* **Amazon VPC** – Network infrastructure
* **Security Groups** – Network access control
* **AWS Systems Manager Session Manager** – EC2 instance management
* **Amazon S3** – Application file storage

## Technologies Used

* React.js
* Node.js
* Express.js
* Nginx
* MySQL
* PM2
* Linux
* Git
* AWS

## Web Tier

The Web Tier was deployed on Amazon EC2 and used **Nginx** to serve the React frontend.

Nginx was also configured as a reverse proxy for API requests.

```text
Browser
   |
   v
Nginx
   |
   +----> React Frontend
   |
   +----> Internal Load Balancer
```

## Application Tier

The backend was developed using **Node.js and Express.js**.

The application listened on:

```text
Port: 4000
```

A health check endpoint was configured at:

```text
/health
```

The backend handled transaction-related operations and communicated with the MySQL database.

**PM2** was used to manage the Node.js application process.

## Database Tier

**Amazon RDS MySQL** was used as the database for storing application transaction data.

The backend communicated with RDS to perform database operations such as:

* Adding transactions
* Retrieving transactions
* Deleting transactions
* Retrieving transactions by ID

## Networking

The application was deployed inside an **Amazon VPC** with controlled communication between the different components.

Security Groups were configured to allow only the required traffic between the Web Tier, Internal Load Balancer, Application Tier, and database.

The backend target group was configured to use:

```text
Protocol: HTTP
Port: 4000
Health Check: /health
```

## Nginx Reverse Proxy

Nginx was configured to serve the React application and forward API requests to the internal Application Load Balancer.

This created the following request path:

```text
Client
  ↓
Nginx
  ↓
Internal ALB
  ↓
Node.js Backend
  ↓
RDS MySQL
```

## Project Demo

The AWS environment was used for the deployment and testing of the application.

The infrastructure is **not currently running** because AWS resources can generate ongoing costs when left active.

The video included in this repository demonstrates the application working during the deployment.

### Demo Video

**AWS Cloud Application – Working Demo**

`demo/aws-cloud-application-demo.mp4`

## What I Learned

This project gave me hands-on experience with:

* AWS EC2
* Amazon RDS
* Amazon VPC
* Application Load Balancer
* Security Groups
* Nginx
* React.js
* Node.js and Express.js
* PM2
* Linux server administration
* Reverse proxy configuration
* Backend and database connectivity
* AWS Systems Manager
* Troubleshooting AWS application connectivity

## Troubleshooting Experience

During the deployment, I worked through connectivity and configuration issues between the Web Tier, Internal Load Balancer, and Application Tier.

One important configuration was aligning the backend application port with the target group:

```text
Node.js Application → Port 4000
Target Group        → Port 4000
Health Check        → /health
```

This helped me understand how application-level configuration and AWS networking work together.

## Future Improvements

Possible improvements for this project include:

* HTTPS using AWS Certificate Manager
* Route 53 domain configuration
* CI/CD pipeline
* Infrastructure as Code using Terraform
* CloudWatch monitoring and logging
* Docker containerization
* Automated deployment
* Improved application security

## Project Status

**Completed**

The project was successfully deployed and tested on AWS. The live infrastructure has been stopped after completion to avoid unnecessary ongoing AWS costs.

The repository contains the project documentation and working demonstration video.

## Author

**Keshav Kumar Sekhri**

### Areas of Interest

**AWS | Cloud Computing | DevOps | Linux | Networking | Infrastructure**
