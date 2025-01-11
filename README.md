![Screenshot 2025-01-12 021436](https://github.com/user-attachments/assets/32f1e551-0706-4c8a-b4c2-e444ce65b371) 

### AWS_architecture_self_activity

![Static Badge](https://img.shields.io/badge/Windows-orange)
![Static Badge](https://img.shields.io/badge/MicrosoftPowerpoint-purple)

## Scenario
You have a web application that accepts requests from the internet. Clients can send requests to query for data. When a request comes in, the web application queries a MySQL database and returns the data to the client.

## Problem Statement
Design a three-tier architecture that follows AWS best practices by using services such as Amazon Virtual Private Cloud (Amazon VPC), Amazon Elastic Compute Cloud (Amazon EC2), Amazon Relational Database Service (Amazon RDS) with high availability, and Elastic Load Balancing (ELB). Create an architecture diagram that lays out your design, including the networking layer, compute layer, database layer, and anything else that’s needed to accurately depict the architecture. Write a few paragraphs that explain why you chose the AWS services that you used and how they would support the solution for the given scenario. Your explanation must describe how traffic flows through the different AWS components—from the client to the backend database, and back to the client.

**Three-Tier Architecture Design on AWS**

### **Architecture Diagram**
- **Networking Layer (Amazon VPC)**
  - Create a custom VPC with two public subnets and two private subnets in two different Availability Zones (AZs) for high availability.
  - Use an internet gateway attached to the VPC for external internet access.
  - Use a NAT gateway in each public subnet to allow instances in private subnets to connect to the internet for software updates while preventing inbound connections from the internet.
  - Create security groups and network ACLs to control access at both the instance and subnet levels.

- **Compute Layer (Amazon EC2 + Auto Scaling + Elastic Load Balancing)**
  - Deploy EC2 instances in private subnets across multiple AZs to run the web application.
  - Use an Elastic Load Balancer (ELB) in front of the EC2 instances to distribute incoming client requests across multiple instances for better availability and fault tolerance.
  - Configure an Auto Scaling group for the EC2 instances to automatically scale up or down based on demand.

- **Database Layer (Amazon RDS for MySQL)**
  - Use Amazon RDS with Multi-AZ deployment for MySQL to ensure high availability and failover support.
  - Deploy RDS instances in private subnets to prevent direct access from the internet.
  - Enable automatic backups, point-in-time recovery, and read replicas (if needed) for improved read performance and disaster recovery.

![Screenshot 2025-01-12 010858](https://github.com/user-attachments/assets/e15bc4d4-a3e2-46f2-8d05-6692ac8005e4)

### **Traffic Flow Explanation**
1. **Client Request:**
   A client sends a request to the web application over the internet.

2. **Elastic Load Balancer:**
   The request first reaches the Elastic Load Balancer (ELB), which distributes the request to one of the EC2 instances in the compute layer. The ELB provides high availability by routing traffic to healthy instances only.

3. **EC2 Instances:**
   The selected EC2 instance receives the request and processes it by querying the backend database. These instances are hosted in private subnets for security reasons. They do not have direct internet access, but they can connect to external services through the NAT gateway.

4. **Database Query:**
   The EC2 instance queries the MySQL database hosted on Amazon RDS. Since RDS is deployed in private subnets across multiple AZs, it ensures high availability. The Multi-AZ deployment guarantees that a standby database instance is available in case of failure.

5. **Response to Client:**
   After retrieving the necessary data, the EC2 instance sends the response back to the client through the ELB. The ELB handles secure communication and ensures even load distribution.

### **AWS Services Selection Rationale**

1. **Amazon VPC:**
   A custom VPC allows us to have complete control over the networking environment, including IP address ranges, subnets, route tables, and gateways. By segregating the infrastructure into public and private subnets, we improve both security and performance.

2. **Elastic Load Balancing (ELB):**
   ELB automatically distributes incoming traffic across multiple EC2 instances. It improves the availability of the application and can handle varying levels of incoming traffic by working seamlessly with Auto Scaling.

3. **Amazon EC2 with Auto Scaling:**
   EC2 instances provide scalable compute capacity, and the Auto Scaling feature ensures that the application can handle fluctuations in traffic by dynamically adding or removing instances as needed.

4. **Amazon RDS with Multi-AZ Deployment:**
   Amazon RDS simplifies the management of MySQL databases by automating backups, patching, and high availability through Multi-AZ deployments. This ensures that in case of an AZ failure, the standby instance will automatically take over without downtime.

5. **NAT Gateway:**
   The NAT gateway enables instances in private subnets to initiate outbound connections to the internet while preventing unsolicited inbound connections, thus maintaining a secure network.

### **Conclusion**
This three-tier architecture on AWS ensures high availability, fault tolerance, scalability, and security for the web application. The use of ELB and Auto Scaling enables the compute layer to handle varying traffic loads effectively. Amazon RDS with Multi-AZ deployment ensures database reliability and minimal downtime. By using VPC with proper subnet segmentation and NAT gateways, the architecture ensures secure and efficient network communication. This design follows AWS best practices and can be easily extended to support additional requirements such as caching, content delivery, and monitoring.

### Procedure
# Task1 
Setting the required tools and environment
1. Copy the below link and paste in your browser
   ![Screenshot (538)](https://github.com/user-attachments/assets/ee98fcec-ccce-4e61-b139-63a9814135a9)
2. Download the `Microsoft PPTx toolkit` wait for the download to start.
3. After your download is complete, unzip the file and open it
   ![Screenshot (539)](https://github.com/user-attachments/assets/70c12866-fb29-4367-87b8-32a40b005a38)
# Task2 
1. Using this tool you can open it in microsoft powerpoint on your windows, copy and paste the necessary icons suitable for your architecture
2. First task includes to design a network layer, where i chose the `VPC` address to be `10.0.0.0/20` and subnets `10.0.1.0/20` and so on
   ![Screenshot (541)](https://github.com/user-attachments/assets/cdacefc0-16d9-44b7-b19a-5500fe96769e)

# Task3
1. For compute layer introduce any compute service in my case i will choose `EC2`
2. Now using `auto scaling group` and `ELB` make sure your solution is highly available
   ![Screenshot (542)](https://github.com/user-attachments/assets/48738cdd-636c-4e72-8fd8-5972312c0242)

# Task4
1. Introduce the Amazon RDS and Amazon S3 bucket services.
2. Use RDS instance in private subnets
3. You can introduce many more services such as `Cloudwatch`
   ![Screenshot (543)](https://github.com/user-attachments/assets/85443fd4-41ee-46ce-988d-814b1e11c78e)
