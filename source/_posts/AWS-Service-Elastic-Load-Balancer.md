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

### 2. Types Of Load Balancers
1. Application Load Balancer
2. Network Load Balancer
3. Classic Load Balancer

#### 1.1. Application Load Balancer(ALB)
- This load balancer is specially designed for web applications with HTTP and HTTPS traffic.
- AWS Application Load Balancer(ALB) operates at Layer 7 of the OSI Model. At Layer 7, the ELB has the ability to inspect application-level content, not just IP and port. This lets it route based on more complex rules than with the Classic Load Balancer. 
For example, an ELB at a given IP will receive a request from the client on port 443(HTTPS). The Application Load Balancer will process the request, not only by receiving port, but also by looking at the destination URL. 
    - Application Load Balancer will be aware of each of these URLs based on patterns set up when configuring the load balancer, and can route to different clusters of servers depending on application need. Rules can also be added at a later time as you add new functionality to your stack. 
	- The Application Load Balancer also integrates with EC2 Container Service(ECS) using Service Load Balancing. This allows for dynamic mapping of services to ports as specified in the ECS task definition. Multiple containers can be targeted on the same EC2 instance, each running different services on different ports. The ECS task scheduler will automatically add these tasks to the ALB. 
- It also provides advanced routing features such as host-based and path-based routing and also works with containers and microservices.
##### Key ALB Concepts
There are some key concepts that you will need to know when configuring your ALB. The first is rules. Each rule specifies a condition, target group, and a priority.
- Rules determine what action is taken when a rule matches a client request. Up to 10 URL-based rules can be defined in the ALB.
	- The condition is the path pattern you want the ALB to evaluate in order for it to route requests. 
- The target group is used to route requests to registered targets as part of an action for a rule. Target groups specify a protocol and target port. Health checks can be configured per target group. An ALB can route to multiple target groups.
	- Targets specify the endpoints and are registered with the ALB as part of a target group.
- Priority tells the ALB in which order to evaluate the rules. Rules are numerically evaluated in order from lowest to highest value. When a rule matches a request, traffic will be routes to the specified target group.
		
