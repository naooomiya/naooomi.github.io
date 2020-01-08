---
title: AWS Service | Elastic Load Balancer
date: 2020-01-07 23:51:16
tags:
    - [AWS Services]
    - [Elastic Load Balancer]
    - [ELB]
    - [AWS Certified Developer - Associate]
categories:
    - [AWS Services]
    - [Elastic Load Balancer]
    - [AWS Certified Developer - Associate]
---

### 1. What is Elastic Load Balancer
Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP address, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zone. Elastic Load Balancing offers three types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant. 

<!-- more -->

---

### 2. Types Of Load Balancers
1. Application Load Balancer
2. Network Load Balancer
3. Classic Load Balancer

#### 1.1. Application Load Balancer(ALB)
- Application Load Balancer is specially designed for load balancing of **HTTP** and **HTTPS** traffic.
- They operate at Layer 7 and are application-aware.
- They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers. 
- It also provides advanced routing features such as host-based and path-based routing and also works with containers and microservices.
	
##### Understanding the Application Load Balancer
AWS Application Load Balancer(ALB) operates at **Layer 7** of the OSI Model. At Layer 7, the ELB has the ability to inspect application-level content, not just IP and port. This lets it route based on more complex rules than with the Classic Load Balancer. 
For example, an ELB at a given IP will receive a request from the client on port **443(HTTPS)**. The Application Load Balancer will process the request, not only by receiving port, but also by looking at the destination URL. 
- Application Load Balancer will be aware of each of these URLs based on patterns set up when configuring the load balancer, and can route to different clusters of servers depending on application need. Rules can also be added at a later time as you add new functionality to your stack. 
- The Application Load Balancer also integrates with EC2 Container Service(ECS) using Service Load Balancing. This allows for dynamic mapping of services to ports as specified in the ECS task definition. Multiple containers can be targeted on the same EC2 instance, each running different services on different ports. The ECS task scheduler will automatically add these tasks to the ALB. 
	
##### Key ALB Concepts
There are some key concepts that you will need to know when configuring your ALB. The first is **rules**. Each rule specifies a **condition**, **target group**, and a **priority**.
- **Rules** determine what action is taken when a rule matches a client request. Up to 10 URL-based rules can be defined in the ALB.
	- The **condition** is the path pattern you want the ALB to evaluate in order for it to route requests. 
- The **target group** is used to route requests to **registered targets** as part of an action for a rule. Target groups specify a protocol and target port. Health checks can be configured per target group. An ALB can route to multiple target groups.
	- **Targets** specify the endpoints and are registered with the ALB as part of a target group.
- Priority tells the ALB in which order to evaluate the rules. Rules are numerically evaluated in order from lowest to highest value. When a rule matches a request, traffic will be routes to the specified target group.

---

#### 1.2. Network Load Balancer 
- Network Load Balancers are best suited for load balancing of **TCP traffic** where extreme performance is required.
- Operating at the connection **level(Layer 4)**
- Network Load Balancer are capable of handling millions of requests per second, while maintaining **ultra-low latencies**. 
- Use for **extreme performance**. The most costly load balancer of the three load balancers. 

##### Understanding the Classic Load Balancer
This load balancer operates at the **Network layer** of the OSI model. 
Suppose your company's website is running on four m4-xlarge instances and you're using an ALB to distribute the traffic among them.
Now your company launched a new product today which got viral and your website starts to get millions of requests per second. 
In this case, the ALB may not be able to handle the sudden spike in traffic.
This is where the NLB really shines. It has the capability to handle a sudden spike in traffic since it works at the connection level. It also provides support for **static IPs**.

---

#### 1.3. Classic Load Balancer
- Classic Load Balancers are the *legacy* Elastic Load Balancers.
- You can load balance **HTTP/HTTPS** applications and use **Layer 7-specific** features, such as **X-Forwarded** and **sticky sessions**.
- You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol. 
- If your application stops responding, the ELB(Classic Load Balancer) responds with a **504 error**. This  means that the application is having issues. This could be either at the **Web Server Layer** or at the **Database Layer**. Identify where the application is failing, and scale it up or out where possible. 

##### Understanding the Classic Load Balancer
The Classic EBL has a number of features available to help provide *high availability, monitoring, and better security* for your application stack.
The AWS Classic Load Balancer(CLB) operates at **Layer 4** of the OSI model. What this means is that the load balancer routes traffic between clients and backend servers based on IP address and TCP port.
For example, an ELB at a given IP address receives a request from a client on **TCP port 80(HTTP)**. It will then route that request based on the rules previously configured when setting up the load balancer to a specified port on one of a pool of backend servers. In this example, the port on which the load balancer routes to the target server will often be **port 80(HTTP) or 443(HTTPS)**.

The backend destination server will then fulfil the client request, and send the requested data back to the ELB, which will then forward the backend server reply to the client. From the client's perspective, this request will appear to have been entirely fulfilled by the ELB. The client will have no knowledge of the backend server or servers fulfilling client requests.

##### X-Forwarded-For Header

**Request**(124.12.3.231) ---> **Load Balancer**(10.0.0.23) ---> **EC2 Instance**(10.0.0.23)(X-Forwarded-For: 124.12.3.231)

The request comes from a public IP address(124.12.3.231) then it hits the load balance. The load balance take the request and use private IP address(10.0.0.23) to send to EC2 instance. Now EC2 instance will only see the private IP address(10.0.0.23). Now you probably want to know where in the world it comes from. So how to get the public IP address when the Elastic Load Balancer sending a private address? The answer will be **X-Forwarded-For**.

---

### 3. ELB Exam Tips
- 3 Types of Load Balancers:
	- Application Load Balancers
	- Network Load Balancers
	- Classic Load Balancers
- 504 Error means the gateway has timed out. This means that the application not responding within the idle timeout period.
	- Trouble shoot the application. Is it from the Web Server or Database Server?
- If you need the **IPv4 address** of your end user, look for the **X-Forwarded-For** header. 
	
	
