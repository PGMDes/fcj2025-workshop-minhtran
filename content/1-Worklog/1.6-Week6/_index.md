---
title: "Week 6 Worklog"
date: "2025-10-13"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Review foundational database (DB) concepts, including RDBMS (primary key, foreign key), optimization techniques (Index, Partition), and operational concepts (Database Log, Buffer).
- Clearly differentiate between the two main DB system types: **OLTP** (Online Transaction Processing) and **OLAP** (Online Analytical Processing or Data Warehouse).
- Understand the managed relational database service **Amazon RDS**, including core features like **Multi-AZ** (for high availability) and **Read Replicas** (for read performance).
- Learn about **Amazon Aurora**, AWS's cloud-native DB service, with its unique shared storage architecture, high performance, and superior features like **Zero Replication Lag**.
- Learn about **Amazon Redshift**, the petabyte-scale Data Warehouse service designed for OLAP, and understand its **MPP** architecture and **Columnar Storage** technique.
- Understand the role of **Amazon ElastiCache** (Redis, Memcached) as a high-speed caching layer to reduce load on the primary database.

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Database Concepts:**<br>- RDBMS architecture (PK, FK, Normalization) & Optimization (Index, Partition, Execution Plan).<br>- **RDBMS (ACID)** vs. **NoSQL (BASE)**.<br>- Workloads: **OLTP** (Transactional) vs. **OLAP** (Analytical). | 13/10/2025 | 13/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| Tue | **Amazon RDS:**<br>- Managed service features, Automated Backups.<br>- **Multi-AZ:** Synchronous replication for High Availability.<br>- **Read Replicas:** Asynchronous replication for Read Scaling. | 14/10/2025 | 14/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| Wed | **Amazon Aurora:**<br>- Storage Architecture: Shared Volume, 6 copies across 3 AZs, Zero Lag.<br>- Cluster Structure: 1 Writer + up to 15 Readers.<br>- Features: Backtrack, Global Database. | 15/10/2025 | 15/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| Thu | **Amazon Redshift:** Data Warehouse, MPP architecture, Columnar Storage for OLAP, Redshift Spectrum.<br>**Amazon ElastiCache:** In-memory caching (Redis/Memcached) to offload primary DB. | 16/10/2025 | 16/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| Fri | **Lab 000005:** Amazon RDS Basics (Create, Connect, Backup/Restore).<br>**Lab 000043:** DB Migration using DMS & SCT (Oracle to Aurora).<br>**Extra Study:** *Database Internals* & *The Data Warehouse Toolkit* books. | 17/10/2025 | 17/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |

### Week 6 Achievements:

- **Lesson (Foundational):**
  + Clearly differentiate between the two system models: **OLTP** (Online Transaction Processing) and **OLAP** (Online Analytical Processing, data warehouse).
  + Master basic DB optimization techniques: **Index** (speeds up reads) and **Partition** (divides tables).
  + Understand the role of **Database Log** (for recovery/replication) and **Buffer** (uses RAM for speed).
- **Service (RDS):**
  + Know **Amazon RDS** is a managed relational database (OLTP) service.
  + Clearly distinguish RDS's 2 main features: **Multi-AZ** (used for High Availability - HA) and **Read Replicas** (used to increase read performance).
- **Technique (Replication):**
  + Differentiate **Synchronous Replication** (used for RDS Multi-AZ) and **Asynchronous Replication** (used for RDS Read Replicas, can have lag).
- **Service (Aurora):**
  + Know **Amazon Aurora** is a high-performance, cloud-native database.
  + Understand Aurora's **shared storage (Cluster Volume)** architecture and its superior benefit of **Zero Replication Lag**.
  + Be aware of advanced features like **Backtrack** and **Global Database**.
- **Service (Redshift):**
  + Know **Amazon Redshift** is a data warehouse (OLAP) service.
  + Understand the **MPP (Massively Parallel Processing)** architecture (includes Leader Node and Compute Nodes).
  + Master the core technique of OLAP: **Columnar Storage**, which speeds up analytical queries.
- **Service (ElastiCache):**
  + Know **Amazon ElastiCache** (Redis/Memcached) is an in-RAM caching service.
  + Understand the role of caching is to reduce load on the primary DB.
  + Be aware of the responsibility to write the **Caching Logic** in the application.
- **Hands-on:**
  + Know how to create and operate (backup/restore) an **RDS** database.
  + Know how to use DMS and SCT services to **migrate** a DB from Oracle to Aurora.