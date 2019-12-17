---
title: AWS Service | IAM101
date: 2019-12-17 22:55:56
tags:
    - [AWS Services]
    - [IAM]
categories:
    - [AWS Services]
    - [IAM]
    - [AWS Certified Developer - Associate]
---

### What is IAM
Essentially, IAM allows you to manage users and their level of access to the AWS Console. It is important to understand IAM and how it woks, both for the exam and for administrating a company's AWS account in real life. 

<!-- more -->

### What does IAM give you
- **Centralized control of your AWS account**
- **Shared Access to your AWS account**
- **Granular Permissions**
    - It means you can enable different levels of access to different users within your organization
- **Identity Federation** (including Active Directory, Facebook, LinkedIn, etc) 
	- This means it can enable users to log in using credentials stored in an Active Directory, Facebook or LinkedIn
- **Multifactor Authentication**
	- This is where a user is granted access only after successfully completing multiple independent authentication mechanisms. For example, providing a username and password as one authentication mechanism and then providing a software token site that could be via a token generator like Google Authenticator as the second authentication mechanism
- **Provides temporary access for users/devices and services, as necessary**
	- For example, if you developed a web or mobile phone application you can configure identity access management to enable users to have temporary access to AWS resources within your account. For example, to enable access to store or retrieve data located in an S3 bucket or within a Dynamo DB database.
- **Allows you to set up your own password rotation policy**
- **Integrates with many different AWS services**
- **Supports PCI DSS Compliance**
	- for applications associated with the payment card industry

---

### Critical Terms
- **Users** - End Users (think people)
	- So these are the people logging into the AWS console and also interacting with AWS by running API commands.  
- **Groups** - A collection of users under one set of permissions
	- For example, your marketing team might need access to read and write certain files stored in S3 bucket and that might be logos or images etc. And they're going to need a specific set of permissions to allow them to do this. So it makes sense to create a group with the required permissions and then all you need to do is add the relevant users into that group and they will all have permissions to read the S3 bucket.
- **Roles** - Your create roles and can then assign them to AWS resources
	- A role is used to define a set of permissions for example S3 bucket access and then that role could be assumed by either uses or AWS services such as EC2. So you might have an EC2 instance which needs to query a database or access files in S3 you can configure that using a role. 
- **Policies** - A document that defines one (or more) permissions
	- A policy can be attached to either a user , group or role. 
	- When we attach a policy the user, group or the role will then have the permissions defined within that policy. 
	- It's possible for a user, a group and a role to all share the same policy. 
