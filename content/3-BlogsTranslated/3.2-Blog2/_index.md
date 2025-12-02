---
title: "Blog 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# **Improving Weather Forecast Accuracy with GPU-Accelerated Amazon AppStream 2.0 Instances**

*By Rayette Toles-Abdullah, Austin Park, and Chris Quarcoo | May 13, 2025 | related: [Amazon AppStream 2.0](https://aws.amazon.com/pm/appstream2/), [Best Practices](https://aws.amazon.com/blogs/publicsector/category/post-types/best-practices/), [Customer Solutions](https://aws.amazon.com/blogs/publicsector/category/post-types/customer-solutions/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/)*

![image1](/images/3-BlogsTranslated/06.png)

Access to applications and data from anywhere and on any device is increasingly important for distributed, remote, and connectivity-constrained workforces. Field researchers and meteorologists around the world rely on real-time data ingestion for critical weather capabilities.

The Advanced Weather Interactive Processing System (AWIPS) is a weather forecasting and visualization system used by the U.S. National Weather Service (NWS) and meteorological agencies worldwide. AWIPS enables meteorologists to monitor, analyze, and forecast weather patterns with high accuracy, producing better forecasts and more effective warnings to help protect life and property. AWIPS ingests data from multiple sources—satellites, radar, and sounding balloons. The Common AWIPS Visualization Environment (CAVE) is the client application forecasters use to interact with AWIPS. CAVE receives processed data from AWIPS servers and provides visualization tools for forecasting, issuing alerts, and exploring weather data.

This post shows how to stream the Common AWIPS Visualization Environment (CAVE) using [Amazon AppStream 2.0](https://aws.amazon.com/pm/appstream2/) — a managed application streaming service that lets you stream desktop applications from AWS to any device without additional local hardware or software.

## Benefits of running GPU‑intensive applications on Amazon AppStream 2.0

AppStream 2.0 offers several advantages:

- Users can access desktop applications from any supported device, including laptops, desktops, tablets, and phones—providing mobility and flexibility to remain productive whether in the office, at home, or on the move.
- You can scale GPU capacity up and down on demand, optimizing costs by paying only for what you use and avoiding the expense of idle hardware.
- There’s no need to overprovision GPU capacity, which is valuable for organizations with variable or seasonal workloads.
- Users can access GPU‑accelerated applications from any device, including mobile devices, delivering consistent performance regardless of the end device’s local capabilities.
- AppStream 2.0 handles GPU driver management, GPU fleet orchestration, and GPU‑optimized application stacks, reducing IT operational burden so teams can focus on strategic initiatives.
- GPU usage in AppStream 2.0 is pay-as-you-go, eliminating high upfront capital expenditure for physical GPU servers and lowering the barrier for organizations to adopt GPU workloads.
- AppStream 2.0 provides instance types optimized for graphics workloads such as Graphics G4dn and Graphics G5 powered by NVIDIA GPUs, enabling high performance for 3D modeling, video editing, and similar tasks.
- GPU workloads and data never reside on the user’s device; they remain isolated in the AWS Cloud, improving security and compliance for sensitive applications and providing centralized control over data access and IP protection.

![image2](/images/3-BlogsTranslated/07.png)  
Figure 1. AWIPS CAVE visualization of Hurricane Lee on 2023-09-13 using Amazon AppStream 2.0.

## Explore the AWIPS solution

The AWIPS CAVE workstation is the primary interface forecasters use. AWIPS CAVE system requirements include:

- OpenGL 2.0 compatible device  
- Minimum 4 GB RAM  
- Minimum 2 GB disk space for cache  
- NVIDIA graphics card  
- Latest NVIDIA drivers

To configure AWIPS for Amazon AppStream 2.0, the steps include:

### Create a Linux-based image

Prepare a Linux environment and install AWIPS CAVE and its dependencies. This becomes the base for streaming the application.

![image3](/images/3-BlogsTranslated/08.png)

### Create an application optimization manifest

AppStream 2.0 uses manifest files to optimize streaming performance by preloading required files. This script identifies all runtime files CAVE needs.

![image4](/images/3-BlogsTranslated/09.png)

### Add the application to the AppStream catalog

Register CAVE in the AppStream application catalog, specifying launch path, display name, and the optimization manifest you created.

![image5](/images/3-BlogsTranslated/10.png)

### Configure the fleet

Create a fleet to manage the instances that will run your streamed application. Choose between on-demand (cost-efficient) or always-on (instant availability).

- Recommended: Graphics G4dn (stream.graphics.g4dn.xlarge) or Graphics Pro (stream.graphics-pro.4xlarge)  
- Choose an On‑demand fleet  
- Set desired capacity limits

### Create the image

Build the final Amazon AppStream image that will be used to launch streaming sessions. This captures installed applications and configuration.

![image6](/images/3-BlogsTranslated/11.png)

### Configure user authentication

Choose between managing users directly in AppStream or integrating with your existing identity provider.

- Configure an Amazon Cognito user pool  
- Integrate AppStream with AWS Identity Center

The diagram below shows a high-level architecture of the solution.

![image7](/images/3-BlogsTranslated/12.png)

Figure 2. High-level architecture showing Amazon AppStream 2.0, Amazon S3, Amazon EFS, Amazon Aurora, and Amazon EC2.

## AWIPS use cases beyond the field

NWS River Forecast Centers (RFCs) use AWIPS CAVE to monitor and forecast river stages, issue flood warnings, and provide hydrology information and drought conditions. Weather Forecast Offices (WFOs) rely on AWIPS CAVE for local forecasts, alerts, and advisories, coordinating with other WFOs, federal/state agencies, and private partners. The NWS National Hurricane Center (NHC) uses AWIPS CAVE for tropical cyclone monitoring and forecasting, supporting timely public information for emergency managers and stakeholders. Universities and research institutes also use AWIPS CAVE for research, teaching, and training in meteorology and atmospheric sciences.

## Conclusion

Integrating AWIPS CAVE with Amazon AppStream 2.0 is a significant step forward for accessibility and forecasting capability. This solution addresses growing demand for remote access to mission‑critical meteorological applications, while delivering flexibility, cost efficiency, and performance.

By leveraging cloud compute and GPU acceleration, meteorologists and researchers can access advanced weather analysis tools from anywhere on any device. This improves forecast accuracy and timeliness and enhances overall service effectiveness.

As weather patterns grow more complex and climate challenges continue, innovations like this play a key role in supporting forecasters and improving community safety and preparedness.

**About the authors**
| :---- | :---- |
| ![image8](/images/3-BlogsTranslated/13.jpg) | **Rayette Toles-Abdullah** — Principal Solutions Architect, Worldwide Public Sector Federal Civilian, AWS. Rayette has 23+ years of experience in systems integration, application modernization, and delivering high‑impact solutions to meet mission and business needs. |
| ![image9](/images/3-BlogsTranslated/14.png) | **Austin Park** — Solutions Architect, Worldwide Public Sector Federal Civilian, AWS. Austin has 2+ years of experience, specializing in storage systems and helping customers migrate to the cloud. |
| ![image10](/images/3-BlogsTranslated/15.jpg) | **Chris Quarcoo** — Solutions Architect, Worldwide Public Sector, AWS. Chris has 4+ years of industry experience focusing on cloud operations and container technologies, designing and deploying cloud solutions for government and public sector organizations. |

