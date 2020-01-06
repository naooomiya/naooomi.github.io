---
title: AWS Service | EC2 101
date: 2020-01-06 21:53:47
tags:
    - [AWS Services]
    - [EC2]
    - [AWS Certified Developer - Associate]
categories:
    - [AWS Services]
    - [EC2]
    - [AWS Certified Developer - Associate]
---

### 1. What is EC2(Virtual Server)?
- Amazon Elastic Compute Cloud(Amazon EC2) is a web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change. <!-- more -->
    - (It's just virtual machines in the cloud and it reduces the time required to obtain and boot new server)
- Amazon EC2 changes the economics of computing by allowing you to pay only for capacity that you actually use. Amazon EC2 provides developers the tools to build failure resilient applications and isolate themselves from common failure scenarios. 

---

### 2. EC2 Options
- **On Demand** 
    - allows you to pay a fixed rate by the hour (or by the second) with no commitment.
- **Reserved** 
    - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. 1 Year or 3 Year Terms.
- **Spot** 
    - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times.
- **Dedicated Hosts** 
    - Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses. 
	

#### 2.1. On Demand
- Perfect for users that want the low cost and flexibility of Amazon EC2 without any up-front payment or long-term commitment.
- Applications with short term, spiky, or unpredictable workloads that cannot be interrupted.
- Applications being developed or tested on Amazon EC2 for the first time. 

#### 2.2. Reserved Instances
- Applications with steady state or predictable usage
- Applications that require reserved capacity
- Users can make up-front payments to reduce their total computing costs even further
	- Standard RIs(Reserved Instances)(Up to 75% off on-demand)
	- Convertible RIs(Up to 54% off on-demand) feature the capability to change the attributes of the RI as long as the exchange results in the creation of Reserved Instances of equal or greater value.
	- Scheduled RIs are available to launch within the time window you reserve. This option allows you to match your capacity reservation to a predictable recurring schedule that only requires a fraction(一小部分) of a day, a week, or a month. 

#### 2.3. Spot Instances
- Applications that have flexible start and end times
- Applications that are only feasible at very low compute prices
	- Some chemical companies or big pharmaceutical companies use this spot instances to do huge amounts of computing at like 4 am on Sunday morning and this can save a lot of money compared to using the same compute capacity from like 9-5 during the week. 
- Users with an urgent need for large amounts of additional computing capacity
	
#### 2.4. Dedicated Hosts
- Useful for regulatory requirements that may not support multi-tenant virtualization.
- Great for licensing which does not support multi-tenancy or cloud deployments
- Can be purchased On-Demand(hourly)
- Can be purchased as a Reservation for up to 70% off the On-Demand price. 

---

### 3. EC2 Instance Type
	
|    | Family | Speciality | Use Case |
|:--:|:------:|:----------:|:--------:|
| 1  | **F1** | **Field Programmable Gate Array** | Genomics Research, Financial Analytics, Real-time video processing, Big Data, etc |
| 2  | **I3** | **High Speed Storage** | NoSQL DBs, Data Warehousing, etc |
| 3  | **G3** | **Graphics Intensive** | Video Encoding/3D Application Streaming |
| 4  | **H1** | **High Disk Throughput** | MapReduce-based workloads, Distributed file system such as HDFS and MapR-FS |
| 5  | **T2** | **Lowest Cost, General Purpose** | Web Servers/Small DBs |
| 6  | **D2** | **Dense Storage** | Fileservers/Data Warehousing/Hadoop |
| 7  | **R4** | **Memory Optimized** | Memory Intensive Apps/DBs |
| 8  | **M5** | **General Purpose** | Application Servers |
| 9  | **C5** | **Compute Optimized** | CPU Intensive Apps/DBs |
| 10 | **P3** | **Graphics/General Purpose GPU** | Machine Learning, Bit Coin Mining, etc |
| 11 | **X1** | **Memory Optimized** | SAP HANA/Apache Spark, etc |

#### How to remember: 
**F** - **FPGA** (Field Programmable Gate Array)
**I** - **IOPS** (High Speed Storage)
**G** - **Graphics** (Graphics Intensive)
**H** - **High Disk Throughput**
**T** - **Cheap general purpose** (Lowest Cost, General Purpose)
**D** for **Density** (Dense Storage)
**R** for **RAM** (Memory Optimized)
**M** - main choice for **general purpose** apps (General Purpose)
**C** for **Compute** (Compute Optimized)
**P** - **Graphics/General Purpose GPU** (Pics)
**X** - **Extreme Memory** (Memory Optimized)

---

### 4. What is EBS(Virtual Disk)?
**Amazon EBS(Elastic Block Storage)** allows you to create storage volumes and attach them to Amazon EC2 instances. Once attached, you can create a file system on top of these volumes, run a database, or use them in any other way you would use a block device. Amazon EBS volumes are placed in a specific Availability Zone, where they are automatically replicated to protect you from the failure of a single component. 

---

### 5. EBS Volume Types
- **General Purpose SSD(GP2)**
	- General purpose, balances both price and performance.
	- Ratio of 3 IOPS(Input/Output Operation Per Seconds) and the ability to burst up to 3000 IOPS for extended periods of time for volumes at 334 GB and above.
- **Provisioned IOPS SSD(IO1)**
	- Designed for I/O intensive applications such as large relational or NoSQL databases
	- Use if you need more than 10, 000 IOPS
	- Can provision up to 20, 000 IOPS per volume
- **Throughput Optimized HHD(ST1)**
	- Big  data
	- Data Warehouses
	- Log processing
	- Cannot be a boot volume have to be additional volume
- **Cold HDD(SC1)**
	- Lowest Cost Storage for infrequently accessed workloads
	- File Server
	- Cannot be a boot volume
- **Magnetic(Standard)**
	- Lowest cost per gigabyte of all EBS volume types that is bootable. Magnetic volumes are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important. 
		
---

### EC2 Exam Tips
#### 1. EC2 Options
- On Demand - allows you to pay a fixed rate by the hour (or by the second) with no commitment
- Reserved - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. 1 Year or 3 Year Terms
- Spot - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. 
- Dedicated Hosts - Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses. 

#### 2. If a Sport instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for the complete hour in which the instance ran. 
#### 3. SSD
a. *General Purpose SSD* - balances price and performance for a wide variety of workloads
b. *Provisioned IOPS SSD* - Highest - performance SSD volume for mission-critical low-latency or high-throughput workloads
#### 4. Magnetic
a. *Throughput Optimized HDD* - Low cost HDD volume designed for frequently accessed, throughput-intensive workloads
b. *Cold HDD* - Lowest cost HDD volume designed for less frequently accessed workloads
c. *Magnetic* - Previous Generation. Can be a boot volume. 