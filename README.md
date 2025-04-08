#  Razorpay Architecture on AWS

Razorpay is one of India's leading fintech platforms, providing secure and scalable payment gateway services to over 30,000 merchants. This project outlines the high-level cloud-native architecture used by Razorpay, leveraging various AWS services for scalability, availability, and security.

---

##  Overview

Razorpay uses AWS to deploy and manage its payment gateway, achieving:

- High Availability  
- Scalable Microservices  
- Secure Transactions  
- Automated CI/CD Pipelines

---

##  AWS Services Used

| Category              | AWS Service(s) Used                                   |
|-----------------------|-------------------------------------------------------|
| Frontend Hosting      | Amazon S3, CloudFront                                 |
| DNS & Routing         | Amazon Route 53                                       |
| Authentication        | Amazon Cognito                                        |
| API Management        | Amazon API Gateway                                    |
| Business Logic        | AWS Lambda / EC2                                      |
| Databases             | Amazon RDS, DynamoDB                                  |
| Caching               | Amazon ElastiCache (Redis)                            |
| Notifications         | Amazon SNS                                            |
| Monitoring & Logging  | Amazon CloudWatch                                     |
| Security              | AWS KMS, AWS WAF, AWS Shield, AWS Secrets Manager     |
| CI/CD Automation      | AWS CodePipeline, AWS CodeDeploy                      |

---

##  Workflow

### 1. User Accesses Website
- DNS routing using Amazon Route 53.
- Frontend hosted on Amazon S3 (static site).
- Content delivered globally via Amazon CloudFront.

### 2. User Registration & Login
- Managed by Amazon Cognito.
- JWT token issued upon successful authentication.

### 3. Frontend Triggers Payment Request
- Secure API call via Amazon API Gateway.
- JWT attached for user identity validation.

### 4. Backend Logic Execution
- Lambda/EC2 verifies user token, fetches product data.
- Applies offers/taxes and initiates Razorpay payment session.

### 5. Payment Redirection
- User is redirected to Razorpay Checkout (hosted payment page).
- All sensitive payment actions handled securely by Razorpay UI.

### 6. Database Transactions
- Payment & user data stored in RDS (PostgreSQL/MySQL).
- DynamoDB supports fast queries (logs, dashboards).
- ElastiCache (Redis) for frequently accessed data like coupons.

### 7. Asynchronous Events
- Amazon SNS sends notifications (email/SMS) to users and admins.

### 8. Post-Payment Callback
- Razorpay redirects user to return URL.
- Webhook confirms payment to backend.
- Status updated in DB, user notified.

### 9. Monitoring & Logging
- Amazon CloudWatch monitors all services and Lambda metrics.

### 10. Security & Compliance
- AWS KMS encrypts sensitive data.
- Secrets stored in AWS Secrets Manager.
- AWS WAF & Shield protect against DDoS and web-based attacks.

---

##  Benefits of this Architecture

- Scalable and cost-effective  
- Serverless-ready (via Lambda)  
- Secure and PCI-DSS compliant  
- Easy to audit and debug  
- Integrates multi-payment methods
