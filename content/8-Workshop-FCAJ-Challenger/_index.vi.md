---
title: "Workshop"
date: "2025-09-09"
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

![overview](/images/8-Workshop-FCAJ-Challenger/diagram-architecture-01.jpg)

## 1. Data Ingestion – Data Input → Amazon S3 (Raw Data)

Nguồn dữ liệu ban đầu là dataset Yellow Taxi Trips từ NYC Taxi and Limousine Commission.

| Field                 | Ý nghĩa               |
| --------------------- | --------------------- |
| VendorID              | ID hãng taxi          |
| tpep_pickup_datetime  | Thời gian đón khách   |
| tpep_dropoff_datetime | Thời gian trả khách   |
| passenger_count       | Số hành khách         |
| trip_distance         | Khoảng cách chuyến đi |
| PULocationID          | ID vị trí đón         |
| DOLocationID          | ID vị trí trả         |
| fare_amount           | Giá cước              |
| tip_amount            | Tiền tip              |
| total_amount          | Tổng tiền             |

Dữ liệu thô được upload vào bucket S3 Raw.

Ví dụ:

    s3://taxi-data-raw/yellow_tripdata_2024_01.parquet

    s3://taxi-data-raw/yellow_tripdata_2024_02.parquet

S3 đóng vai trò:
- Data Lake raw layer
- Lưu parquet / csv gốc
- Chưa xử lý

## 2. Event Detection – S3 → EventBridge
Khi có file mới trong bucket raw:

    PUT Object → S3 Event

event này được gửi tới Amazon EventBridge.

EventBridge phát hiện:

    ObjectCreated

Ví dụ event:
```
{
 "source": "aws.s3",
 "detail-type": "Object Created",
 "bucket": "taxi-data-raw",
 "object": "yellow_tripdata_2024_01.parquet"
}
```

## 3. EventBridge Trigger → Data Processing Workflow
EventBridge kích hoạt workflow xử lý dữ liệu.

Workflow orchestration nằm trong Step Functions.

Service orchestration giúp:
- Điều phối pipeline
- Retry khi lỗi
- Log trạng thái pipeline

## 4. Data Profiling – AWS Glue DataBrew Profile
Step Function gọi AWS Glue DataBrew để data profiling.

DataBrew Profile sẽ phân tích dataset:

Ví dụ với Yellow Taxi dataset:

| Column          | Insight       |
| --------------- | ------------- |
| passenger_count | max=6         |
| trip_distance   | max≈200 miles |
| fare_amount     | có giá trị âm |
| PULocationID    | 263 giá trị   |

Mục tiêu:
- Detect missing values

- Detect outliers

- Detect data type mismatch

Ví dụ:
```
fare_amount < 0

trip_distance = 0

passenger_count = null
```
## 5. Lambda – Pipeline Control
Sau profiling, AWS Lambda được gọi.

Lambda thực hiện:

1️⃣ đọc kết quả profiling

2️⃣ quyết định pipeline step tiếp theo

Ví dụ logic:
```
if null_rate > 20%:
    send_alert()
else:
    start_databrew_recipe()
```
Lambda đóng vai trò:
- orchestration logic

- validation logic

## 6. Data Transformation – Glue DataBrew Recipe
DataBrew Recipe thực hiện ETL transformation.

Các bước transform thường dùng cho dataset taxi:

**Cleaning**
```
remove null passenger_count
remove negative fare
remove trip_distance = 0
```
**Feature Engineering**

Tạo thêm feature:
```
trip_duration = dropoff - pickup
trip_speed = trip_distance / duration
tip_ratio = tip_amount / fare_amount
```
**Data Type Standardization**
```
datetime → timestamp
numeric → float
```
**Partitioning**
```
year
month
day
```
## 7. Store Processed Data – S3 Processed Layer
Data sau khi ETL được lưu vào bucket:
```
s3://taxi-data-processed/
```
Ví dụ:
```
s3://taxi-data-processed/year=2024/month=01/yellow_tripdata.parquet
```
Đây là curated data layer.

Format thường dùng:
- Parquet
- Columnar format
- Tối ưu query analytics

## 8. Data Warehouse Load – Amazon Redshift
Processed data được load vào Amazon Redshift.

Có thể dùng:
```
COPY command
```
Ví dụ:
```
COPY yellow_trip
FROM 's3://taxi-data-processed/'
IAM_ROLE 'RedshiftRole'
FORMAT AS PARQUET;
```
Sau khi load, ta có bảng analytics:
```
fact_taxi_trip
```
Schema ví dụ:
```trip_id
pickup_datetime
dropoff_datetime
trip_distance
fare_amount
tip_amount
total_amount
pickup_zone
dropoff_zone
```
Redshift tối ưu cho:
- OLAP
- BI dashboard
- aggregations

## 9. Visualization – Amazon QuickSight
Dashboard được tạo bằng Amazon QuickSight.

Ví dụ dashboard:

**Trip Demand**
```
Trips per hour
Trips per zone
Trips per day
```
**Revenue**
```
Total fare by zone
Average tip ratio
Revenue per vendor
```
**Spatial Analysis**
```
Pickup heatmap NYC
Dropoff heatmap
```
## Athena (Ad-hoc Query Layer)
Ngoài Redshift, pipeline cho phép truy vấn trực tiếp S3 bằng Amazon Athena.

Athena dùng khi:
- query dữ liệu nhanh
- khám phá dataset
- không cần load vào warehouse

Ví dụ query:
```
SELECT
date_trunc('hour', pickup_datetime) as hour,
count(*) as trips
FROM yellow_trip
GROUP BY hour
ORDER BY hour
```

## Monitoring & Security Layer
Pipeline được giám sát bởi:

**Identity**: AWS Identity and Access Management

**Logging**: AWS CloudTrail

**Metrics**: Amazon CloudWatch

**Alerting**: Amazon Simple Notification Service

Ví dụ:
```
ETL failed → CloudWatch Alarm → SNS → email
```

## Tổng kết Workflow
Pipeline có thể tóm tắt như sau:
```
Data Source
      ↓
S3 Raw Data Lake
      ↓
EventBridge Trigger
      ↓
Step Functions Orchestration
      ↓
Glue DataBrew Profiling
      ↓
Lambda Validation
      ↓
Glue DataBrew ETL
      ↓
S3 Processed Layer
      ↓
Redshift Data Warehouse
      ↓
QuickSight Dashboard
```

## Ý nghĩa kiến trúc
Pipeline này thực hiện modern data lake architecture:

| Layer         | Service        |
| ------------- | -------------- |
| Raw Layer     | S3             |
| Processing    | Glue DataBrew  |
| Orchestration | Step Functions |
| Compute Logic | Lambda         |
| Warehouse     | Redshift       |
| Query         | Athena         |
| BI            | QuickSight     |

Ưu điểm:
- Serverless
- Scalable
- Event-driven
- Cost efficient

#### Nội dung

1. [Tổng quan về Workshop](8.1-Workshop-overview/)
2. [Chuẩn bị môi trường](5.2-Prerequiste/)
3. [Tạo và cấu hình Knowledge Base](5.3-Knowledge-Base/)
4. [Kiểm tra Chatbot (RAG)](5.4-Test-Chatbot/)
5. [Tích hợp ứng dụng Client (Tùy chọn)](5.5-Client-Integration/)
6. [Cập nhật dữ liệu](5.6-Cleanup/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)
