---
title: "Week 5 Worklog"
date: "2025-10-06"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Learn foundational knowledge and core security services on AWS, centered around the "Security is job zero" philosophy.
- Start with the most basic concept: the **Shared Responsibility Model**.
- Focus deeply on managing identity and access (**Identity and Access Management - IAM**), including components: **User**, **Group**, **Policy**, and **Role**.
- Expand learning to identity management services at a larger scale, such as **AWS Organizations** (managing multiple accounts), **AWS Identity Center (SSO)** (single sign-on), and **Amazon Cognito** (user management for web/mobile apps).
- Gain solid knowledge of data protection through encryption with **AWS KMS** and monitoring/compliance checks with **AWS Security Hub**.

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Shared Responsibility Model:** Security *of* the Cloud vs. Security *in* the Cloud.<br>**IAM:**<br>- Root Account protection.<br>- User, Group, Policy types (Identity vs. Resource).<br>- IAM Roles & Assume Role mechanism (STS). | 06/10/2025 | 06/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| Tue | **Amazon Cognito:** User Pools (Authentication) & Identity Pools (Authorization).<br>**AWS Organizations:** Multi-account management, OU, SCPs.<br>**AWS Identity Center (SSO):** Centralized access & Permission Sets. | 07/10/2025 | 07/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| Wed | **AWS KMS:** Encryption key management (CMK, Data Keys).<br>**AWS Security Hub:** Automated security checks & scoring.<br>**Lab 000002:** IAM Basics & Role Assumption.<br>**Lab 000044:** IAM Role Conditions & Restrictions. | 08/10/2025 | 08/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| Thu | **Lab 000048:** IAM Roles for Applications (EC2).<br>**Lab 000030:** Implementing IAM Permission Boundaries.<br>**Lab 000027 & 000028:** Tagging strategies & Resource Groups management. | 09/10/2025 | 09/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| Fri | **Lab 000018:** AWS Security Hub setup & standards check.<br>**Lab 000012:** Configuring AWS SSO with Organizations.<br>**Lab 000033:** KMS Workshop (Encryption, Key Policies).<br>**Extra Study:** AWS Security Specialty Guide. | 10/10/2025 | 10/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) <br> [Research Link](https://www.amazon.com/Certified-Security-Specialty-Guide-SCS-C01/dp/1260461726) |

### Week 5 Achievements:

- **Foundational Lesson:** Master the **Shared Responsibility Model**, clearly understanding AWS's responsibilities versus the customer's.
- **IAM Service (Core):**
  + Clearly distinguish between the **Root Account** (full permissions, needs to be locked away) and **IAM User** (used daily, no permissions by default).
  + Master the 3 main components for granting permissions: **IAM User** (the entity), **IAM Policy** (the permission - written in JSON), and **IAM Group** (a group of entities).
  + Clearly understand **IAM Role**: a mechanism to grant temporary permissions (no permanent credentials) to both Users and Services (like EC2).
- **IAM Techniques (Important):**
  + Know how a User/Service "receives" a Role's permissions through the **Assume Role** technique (using the **STS** service).
  + Understand the permission evaluation rule: An **Explicit Deny** always overrides any Allow permissions.
- **Identity Management Services (Identity Services):**
  + Clearly differentiate between **IAM** (manages AWS administrators) and **Amazon Cognito** (manages end-users of web/mobile apps).
  + Know that **Cognito User Pool** is the user directory (can log in with Facebook, Google) and **Identity Pool** is what grants those users access to AWS resources.
- **Multi-Account Management Service (Multi-Account):**
  + Understand **AWS Organizations** is used for centrally managing multiple accounts, enabling **Consolidated Billing**.
  + Know how to use **Service Control Policies (SCP)** within an Organization to *limit* the maximum permissions of member accounts.
  + Understand **AWS Identity Center (SSO)** as the single sign-on solution, using **Permission Sets** to grant access to accounts within the Organization.
- **Encryption Service (Encryption):**
  + Know **AWS KMS** is the service for creating and managing encryption keys.
  + Understand the **Encryption at Rest** mechanism and differentiate between **CMK** (the master key in KMS) and **Data Key** (the key used to encrypt the actual data).
- **Security Monitoring Service (Monitoring):**
  + Know **AWS Security Hub** is the service that scans and provides security scores, helping to check compliance against standards (like **PCIDSS**).
- **Hands-on:**
  + Practice creating and managing Users, Groups, Policies, and Roles.
  + Practice implementing SSO and KMS.
  + Practice using advanced IAM features like **Conditions** and **Permission Boundaries**.