---
title: "Blog 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# **Hồ dữ liệu địa không gian với Amazon Redshift**

*Bởi Jeremy Spell và Jeff DeMuth | Ngày 10 tháng 7 năm 2025 | liên quan [Amazon Redshift](https://aws.amazon.com/blogs/big-data/category/analytics/amazon-redshift-analytics/), [AWS Glue](https://aws.amazon.com/blogs/big-data/category/analytics/aws-glue/), [AWS Lake Formation](https://aws.amazon.com/blogs/big-data/category/analytics/aws-lake-formation/), [Technical How-to](https://aws.amazon.com/blogs/big-data/category/post-types/technical-how-to/)*

Kiến trúc hồ dữ liệu giúp tổ chức chuyển dữ liệu khỏi các hệ thống lưu trữ cao cấp mà vẫn không mất khả năng truy vấn và phân tích. Cách tiếp cận này hữu ích với dữ liệu địa không gian, khi các nhà xây dựng có thể có hàng terabyte dữ liệu ít truy cập trong cơ sở dữ liệu cần duy trì tiết kiệm chi phí. Tuy nhiên, điều này đòi hỏi công cụ truy vấn hồ dữ liệu phải hỗ trợ kiểu dữ liệu và hàm của hệ thống thông tin địa lý (GIS).

[Amazon Redshift](https://aws.amazon.com/redshift/) hỗ trợ truy vấn [dữ liệu không gian](https://docs.aws.amazon.com/redshift/latest/dg/geospatial-overview.html), bao gồm các kiểu và hàm GEOMETRY và GEOGRAPHY dùng trong truy vấn hệ thống GIS. Ngoài ra, Amazon Redshift cho phép bạn truy vấn dữ liệu địa không gian cả trong hồ dữ liệu trên Amazon S3 và trong kho dữ liệu Redshift, giúp bạn linh hoạt trong cách truy cập dữ liệu. Bên cạnh đó, [AWS Lake Formation](https://aws.amazon.com/lake-formation/) và hỗ trợ [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) trong Eris’s [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview) cung cấp cách kết nối an toàn giữa hồ dữ liệu địa không gian và công cụ trực quan hóa bản đồ. Bạn có thể thiết lập, quản lý, và bảo mật hồ dữ liệu địa không gian trên đám mây chỉ với vài cú nhấp.

Trong bài viết, chúng tôi hướng dẫn cách thiết lập hồ dữ liệu địa không gian bằng Lake Formation và truy vấn dữ liệu với ArcGIS Pro qua [Amazon Redshift Serverless](https://aws.amazon.com/redshift/redshift-serverless/).

## **Tổng quan giải pháp**

Trong ví dụ, một sở y tế quận dùng Lake Formation để bảo vệ hồ dữ liệu chứa dữ liệu thông tin sức khỏe (PHI). Các nhà dịch tễ học muốn tạo bản đồ các phòng khám cung cấp tiêm chủng cho cộng đồng. Các nhà phân tích GIS của quận cần quyền truy cập hồ dữ liệu để tạo bản đồ yêu cầu nhưng không được phép truy cập dữ liệu PHI.

Giải pháp dùng thẻ Lake Formation để cho phép truy cập cấp cột trong cơ sở dữ liệu đối với thông tin công khai gồm tên phòng khám, địa chỉ, mã zip và tọa độ kinh độ/vĩ độ, trong khi không cho phép truy cập dữ liệu PHI trong cùng bảng. Chúng tôi dùng Redshift Serverless và [Amazon Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-getting-started-using-spectrum.html) để truy cập dữ liệu này từ ArcGIS Pro, phần mềm bản đồ GIS của Esri, một đối tác của AWS.

![image1](/images/3-BlogsTranslated/16.png)

Sau đây là lược đồ mẫu cho bài viết.

| Mô tả | Tên cột | Thẻ Geoproperty |
| :---- | :---- | :---- |
| ID bệnh nhân | patient\_id | Không |
| ID phòng khám | clinic\_id | Có |
| Địa chỉ phòng khám | clinic\_address | Có |
| Mã ZIP phòng khám | clinic\_zip | Có |
| Thành phố phòng khám | clinic\_city | Có |
| Tên bệnh nhân | first\_name | Không |
| Họ bệnh nhân | last\_name | Không |
| Địa chỉ bệnh nhân | patient\_address | Không |
| Mã ZIP bệnh nhân | patient\_zip | Không |
| Loại vắc xin | vaccination\_type | Không |
| Vĩ độ phòng khám | clinic\_lat | Có |
| Kinh độ phòng khám | clinic\_long | Có |

Các bước thiết lập giải pháp:

1. Triển khai hạ tầng bằng [AWS CloudFormation](http://aws.amazon.com/cloudformation).  
2. Tải một CSV với dữ liệu mẫu lên bucket [Amazon S3](http://aws.amazon.com/s3) và chạy [AWS Glue](https://aws.amazon.com/glue) crawler để dò dữ liệu.  
3. Thiết lập quyền Lake Formation.  
4. Cấu hình Amazon Redshift Query Editor v2.  
5. Thiết lập schema trong Amazon Redshift.  
6. Tạo view trong Amazon Redshift.  
7. Tạo người dùng cơ sở dữ liệu cục bộ trong ArcGIS Pro.  
8. Kết nối ArcGIS Pro với cơ sở dữ liệu Redshift.

## **Điều kiện tiên quyết**

Bạn cần:

* Tài khoản AWS  
* [Lake Formation được bật ở AWS Region mục tiêu](https://docs.aws.amazon.com/lake-formation/latest/dg/initial-lf-config.html)  
* Hiểu biết về Lake Formation và thiết lập quyền trên bảng  
* [ArcGIS Pro](https://pro.arcgis.com/en/pro-app/latest/get-started/install-and-sign-in-to-arcgis-pro.htm)  
* Kết nối mạng từ client ArcGIS Pro tới VPC nơi tài nguyên Amazon Redshift được triển khai qua [VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html) hoặc [AWS Direct Connect](https://aws.amazon.com/directconnect/)

## **Thiết lập hạ tầng với AWS CloudFormation**

Để tạo môi trường demo, làm theo các bước:

* Đăng nhập [AWS Management Console](http://aws.amazon.com/console) bằng tài khoản quản trị AWS và quản trị hồ dữ liệu Lake Formation-tài khoản này cần vừa là admin của tài khoản vừa là admin của hồ dữ liệu để template hoàn tất.  
* Mở console AWS CloudFormation  
* Chọn [Launch Stack](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create?stackName=geo-sample&templateURL=https://aws-blogs-artifacts-public.s3.amazonaws.com/BDB-3975/infra_setup.yml).

Template CloudFormation tạo các thành phần:

* S3 bucket – `samp-clinic-db-{ACCOUNT\_ID}`  
* AWS Glue database – `samp-clinical-glue-db`
* AWS Glue crawler – `samp-glue-crawler`  
* Redshift Serverless workgroup – `samp-clinical-rs-wg`  
* Redshift Serverless namespace – `samp-clinical-rs-ns`  
* IAM role for Amazon Redshift – `demo-RedshiftIAMRole-{UNIQUE\_ID}`  
* IAM role for AWS Glue – `samp-clinical-glue-role`  
* Lake Formation tag – `geoproperty`

## **Tải CSV lên S3 và chạy AWS Glue crawler**

Tiếp theo, tạo hồ dữ liệu trong môi trường demo, rồi dùng AWS Glue crawler để điền cơ sở dữ liệu AWS Glue và cập nhật schema và metadata trong AWS Glue Data Catalog.

Stack CloudFormation đã tạo sẵn S3 bucket, cơ sở dữ liệu AWS Glue và crawler. Chúng tôi cung cấp bộ dữ liệu thử hư cấu đại diện thông tin bệnh nhân và phòng khám. Tải file và làm theo:

1. Trên console AWS CloudFormation, mở stack vừa khởi chạy.  
2. Ở tab Resources, chọn liên kết tới S3 bucket.  
3. Chọn Upload và tải file CSV (data-with-geocode.csv), rồi chọn Upload.  
4. Trên console AWS Glue, chọn Crawlers trong điều hướng.  
5. Chọn crawler bạn tạo với stack và nhấn Run.  
   Crawler chạy khoảng một phút và sẽ điền bảng tên `clinic-sample-s3\_ACCOUNT\_ID` với dữ liệu hư cấu.  
6. Chọn Tables trong điều hướng và mở bảng crawler đã tạo.

Bạn sẽ thấy tập dữ liệu chứa các trường PHI và thông tin nhận dạng cá nhân (PII).

![image2](/images/3-BlogsTranslated/17.png)

Giờ ta đã có cơ sở dữ liệu và Data Catalog được điền schema và metadata để dùng cho phần còn lại.

## **Thiết lập quyền Lake Formation**

Tiếp theo, chúng tôi minh họa cách bảo vệ dữ liệu PHI để tuân thủ và vẫn hỗ trợ nhà phân tích GIS làm việc hiệu quả. Để bảo vệ hồ dữ liệu, dùng AWS Lake Formation. Để thiết lập đúng quyền Lake Formation, cần hiểu cách truy cập hồ dữ liệu được thiết lập.

Data Catalog cung cấp metadata và schema cho phép dịch vụ truy cập dữ liệu trong hồ. Để truy cập hồ dữ liệu từ ArcGIS Pro, dùng [ArcGIS Pro Redshift](https://pro.arcgis.com/en/pro-app/latest/help/data/databases/connect-redshift.htm) connector, cho phép kết nối từ ArcGIS Pro tới Amazon Redshift. Amazon Redshift có thể truy cập Data Catalog và cung cấp kết nối tới hồ dữ liệu. Template CloudFormation đã tạo Redshift Serverless instance và namespace cùng một vai trò IAM để cấu hình kết nối này. Ta vẫn cần thiết lập quyền Lake Formation để nhà phân tích GIS chỉ truy cập các trường công khai, không truy cập các trường chứa PHI hoặc PII. Ta sẽ gán thẻ Lake Formation cho các cột chứa thông tin công khai và gán quyền cho nhà phân tích GIS để truy cập các cột có thẻ này.

Mặc định, cấu hình Lake Formation cho Super access tới `IAMAllowedPrinciples`; điều này nhằm tương thích ngược như nêu trong [thay đổi cài đặt mặc định cho hồ dữ liệu](https://docs.aws.amazon.com/lake-formation/latest/dg/change-settings.html). Để minh họa cấu hình an toàn hơn, chúng ta sẽ gỡ cấu hình mặc định này.

1. Trên console Lake Formation, chọn **Administration** trong điều hướng.  
2. Trong mục **Data Catalog settings**, đảm bảo **Use only IAM access control for new databases** và **Use only IAM access control for new tables in new databases** không được chọn.  
   ![image3](/images/3-BlogsTranslated/18.png)
3. Trong điều hướng, dưới **Permissions**, chọn **Data permissions**.  
4. Chọn `IAMAllowedPrincipals` và nhấn Revoke.  
5. Chọn **Tables** trong điều hướng.  
6. Mở bảng `clinic-sample-s3\_ACCOUNT\_ID` và chọn **Edit schema**.  
7. Chọn các trường bắt đầu bằng clinic\_ và chọn **Edit LF-Tags**.  
8. Stack CloudFormation đã tạo thẻ Lake Formation tên `geoproperty`. Gán `geoproperty` là khóa và giá trị true cho tất cả các trường `clinic_`, rồi chọn **Save**.  
   Tiếp theo, cấp quyền cho vai trò IAM của Amazon Redshift để truy cập các trường gắn thẻ `geoproperty = true`.  
9. Chọn **Data lake permissions**, rồi chọn **Grant**.  
10. Với IAM role, chọn `demo-RedshiftIAMRole-UNIQUE_ID`.  
11. Chọn `geoproperty` cho khóa và true cho giá trị.  
12. Trong **Database permissions**, chọn **Describe**, và trong **Table permissions**, chọn **Select** và **Describe**.

**Cấu hình Amazon Redshift Query Editor v2**

Tiếp theo, cấu hình ban đầu cho Amazon Redshift cần thiết cho vận hành cơ sở dữ liệu. Chúng tôi dùng một secret của [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) do template tạo để quản lý mật khẩu an toàn theo best practice của AWS.

1. Trên console Amazon Redshift, chọn **Query editor v2**.  
2. Lần đầu khởi chạy Amazon Redshift sẽ hiện cấu hình một lần cho tài khoản. Với bài này, để mặc định và chọn **Configure account**.

Xem thêm các tùy chọn tại [Configuring your AWS account](https://docs.aws.amazon.com/redshift/latest/mgmt/query-editor-v2-getting-started.html).

![image4](/images/3-BlogsTranslated/19.png)

Trình soạn truy vấn cần thông tin xác thực để kết nối tới serverless instance; thông tin này đã được template tạo và lưu trong Secrets Manager.

3. Chọn **Other ways to connect**, rồi chọn **AWS Secrets Manager**.  
4. Ở **Secret**, chọn (`Redshift-admin-credentials`).  
5. Chọn **Save**.  
   ![image5](/images/3-BlogsTranslated/20.png)

**Thiết lập schema trong Amazon Redshift**

External schema trong Amazon Redshift là tính năng tham chiếu schema tồn tại ở nguồn dữ liệu bên ngoài. Tham khảo [External schemas in Amazon Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-spectrum-external-schemas.html) để tạo external schema. Ta dùng external schema để cung cấp quyền truy cập hồ dữ liệu trong Amazon Redshift. Từ ArcGIS Pro, ta sẽ kết nối tới Amazon Redshift để truy cập dữ liệu địa không gian.

Vai trò IAM dùng khi tạo external schema cần được liên kết với namespace Redshift. Việc này đã được template thiết lập, nhưng nên kiểm tra lại trước khi tiếp tục.

1. Trong Redshift Serverless console, chọn **Namespace configuration** ở bảng điều hướng.  
2. Chọn namespace (`sample-rs-namespace`).  
   ![image6](/images/3-BlogsTranslated/21.png)
   Ở tab **Security and encryption**, bạn sẽ thấy vai trò IAM do CloudFormation tạo. Nếu vai trò hoặc namespace không có, hãy kiểm tra stack trong AWS CloudFormation trước khi tiếp tục.  
3. Sao chép ARN của vai trò để dùng sau.  
   ![image7](/images/3-BlogsTranslated/22.png)  
4. Chọn **Query data** để quay lại trình soạn truy vấn.

![image8](/images/3-BlogsTranslated/23.png)

5. Trong query editor, nhập lệnh SQL sau; nhớ thay ví dụ ARN bằng ARN của bạn. Lệnh SQL này tạo external schema dùng cùng vai trò Redshift gắn với namespace để gắn vào cơ sở dữ liệu AWS Glue.  

```
CREATE EXTERNAL SCHEMA samp\_clinic\_sch\_ext FROM DATA CATALOG  
database 'sample-glue-database'  
IAM\_ROLE 'arn:aws:iam::{ACCOUNT\_ID}:role/demo-RedshiftIAMRole-{UNIQUE\_ID}’;  
```

6. Trong query editor, thực hiện truy vấn select trên `sample-glue-database`  
  ``` 
   SELECT * FROM "dev"."samp_clinic_sch_ext"."clinic-sample_s3_{ACCOUNT_ID}";  
  ``` 
   Vì vai trò liên quan đã được cấp quyền truy cập các cột gắn thẻ `geoproperty = true`, chỉ các vùng này sẽ được trả về, thể hiện trong hình ảnh sau (dữ liệu minh họa là hư cấu).  
   ![image9](/images/3-BlogsTranslated/24.png)
7. Dùng lệnh sau để tạo local schema trong Amazon Redshift. External schema không thể cập nhật; ta sẽ dùng local schema để thêm trường hình học với hàm Redshift.  
  ``` 
   CREATE SCHEMA samp_clinic_sch_local
  ```

## **Tạo view trong Amazon Redshift**

Để dữ liệu hiển thị từ ArcGIS Pro, chúng ta cần tạo một view. Sau khi thiết lập schema, ta tạo view có thể truy cập từ ArcGIS Pro.

Amazon Redshift cung cấp nhiều [hàm địa không gian](https://docs.aws.amazon.com/redshift/latest/dg/geospatial-functions.html) dùng để tạo view với các trường mà ArcGIS Pro sử dụng để thêm điểm lên bản đồ. Ta sẽ dùng một hàm vì tập dữ liệu có vĩ độ và kinh độ.

Dùng lệnh SQL sau trong Amazon Redshift Query Editor để tạo view tên `clinic_location_view`. Thay `{ACCOUNT_ID}` bằng ID tài khoản của bạn.
```
CREATE

OR REPLACE VIEW "samp_clinic_sch_local"."clinic_location_view" AS

SELECT

    clinic_id as id,

    clinic_lat as lat,

    clinic_long as long,

    ST_MAKEPOINT(long, lat) as geom

FROM

    “dev”."samp_clinic_sch_ext"."clinic-sample_s3_{ACCOUNT_ID}"

WITH NO SCHEMA BINDING;
```
View mới trong local schema sẽ có cột geom chứa các điểm bản đồ dùng bởi ArcGIS Pro để thêm điểm khi tạo bản đồ. Các điểm trong ví dụ là vị trí phòng khám cung cấp vắc xin. Thực tế, khi phòng khám mới được xây và dữ liệu mới được thêm vào hồ dữ liệu, vị trí của họ sẽ xuất hiện trên bản đồ sử dụng dữ liệu này.

## **Tạo người dùng cơ sở dữ liệu cục bộ cho ArcGIS Pro**

Trong demo, chúng tôi dùng một người dùng và nhóm cơ sở dữ liệu để cấp quyền cho client ArcGIS Pro. Nhập SQL sau trong Amazon Redshift Query Editor để tạo người dùng và nhóm:
```
CREATE USER dbuser with PASSWORD ‘SET_PASSWORD_HERE’;

CREATE GROUP esri_developer_group;

ALTER GROUP esri_developer_group ADD USER dbuser;
```
Sau khi chạy xong, dùng các lệnh sau để cấp quyền cho nhóm:
```
GRANT USAGE ON SCHEMA samp_clinic_sch_local TO GROUP esri_developer_group;

ALTER DEFAULT PRIVILEGES IN SCHEMA samp_clinic_sch_local GRANT SELECT ON TABLES TO GROUP esri_developer_group;

GRANT SELECT ON ALL TABLES IN SCHEMA samp_clinic_sch_local TO GROUP esri_developer_group;
```
## **Kết nối ArcGIS Pro với cơ sở dữ liệu Redshift**

Để thêm các kết nối cơ sở dữ liệu vào ArcGIS Pro, bạn cần endpoint cho workgroup của Redshift Serverless. Bạn có thể xem thông tin endpoint ở trang chi tiết workgroup `sample-rs-wg` trên console Redshift Serverless. Namespace và workgroup Redshift được liệt kê mặc định, thể hiện qua hình ảnh bên dưới.  
![image10](/images/3-BlogsTranslated/25.png)
Bạn có thể sao chép endpoint trong phần **General information**. Endpoint này sẽ cần được chỉnh sửa; đoạn :5439/dev sẽ cần được loại bỏ khi cấu hình connector trong ArcGIS Pro.  
![image11](/images/3-BlogsTranslated/26.png)

1. Mở ArcGIS Pro với dự án bạn muốn thêm kết nối Redshift.

| Đảm bảo đã cài đặt [Amazon Redshift ODBC connector](https://docs.aws.amazon.com/redshift/latest/mgmt/odbc20-install-config-win.html); đây là yêu cầu để kết nối. |
| :---- |

2. Trên menu, chọn **Insert** rồi **Connections**, **Database**, và **New Database Connection**.  
3. Ở **Database Platform**, chọn **Amazon Redshift**.  
4. Ở **Server**, dán endpoint đã sao chép (xóa mọi thứ sau .com khỏi endpoint).  
5. Ở **Database**, chọn cơ sở dữ liệu của bạn.  
   ![image12](/images/3-BlogsTranslated/27.png)

Nếu client ArcGIS Pro của bạn không truy cập được endpoint, bạn sẽ gặp lỗi ở bước này. Một đường mạng giữa client ArcGIS Pro và endpoint Redshift Serverless cần phải được tồn tại. Bạn có thể thiết lập đường mạng với [Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html), [AWS Site-to-Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html), hoặc [AWS Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html). Dù không khuyến nghị vì lí do bảo mật, bạn cũng có thể [cấu hình endpoint công khai](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-console-workgroups.html#serverless-workgroup-describe) cho Amazon Redshift. Hãy tham vấn đội an ninh mạng để có hướng dẫn tốt nhất trước khi cho phép truy cập công khai tới Redshift Serverless.

Nếu có đường mạng mà vẫn lỗi kết nối, kiểm tra security group cho phép inbound từ subnet của ArcGIS Pro qua cổng mà Redshift Serverless dùng. Mặc định là 5439, nhưng có thể cấu hình dải cổng tùy môi trường; xem [Connecting to Amazon Redshift Serverless](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-connecting.html) để biết thêm.

Nếu kết nối thành công, ArcGIS Pro sẽ thêm kết nối Amazon Redshift dưới **Connection File Name**.

1. Chọn **OK**.  
2. Chọn kết nối để hiển thị view đã tạo có geometry (`clinic_location_view`).  
3. Nhấp phải view và chọn **Add To Current Map**.

ArcGIS Pro sẽ thêm các điểm từ view lên bản đồ. Bản đồ cuối cùng được chỉnh ký hiệu để dùng biểu tượng dấu thập đỏ đại diện phòng khám thay vì chấm tròn.

![image13](/images/3-BlogsTranslated/28.png)

## **Dọn dẹp tài nguyên**

Sau khi hoàn tất demo, làm theo bước sau:

1. Trong console Amazon S3, mở bucket do stack CloudFormation tạo và xóa file `data-with-geocode.csv`.  
2. Trong console AWS CloudFormation, xóa stack demo để gỡ các tài nguyên đã tạo.

## **Kết luận**

Bài viết đã hướng dẫn cách thiết lập Redshift Serverless để dùng dữ liệu địa không gian trong hồ dữ liệu nhằm tăng cường bản đồ trong ArcGIS Pro. Kỹ thuật này giúp nhà xây dựng và nhà phân tích GIS tận dụng bộ dữ liệu sẵn có trong hồ dữ liệu và biến đổi trong Amazon Redshift để làm giàu dữ liệu trước khi trình bày trên bản đồ. Chúng tôi cũng cho thấy cách bảo vệ hồ dữ liệu bằng Lake Formation, dò tập dữ liệu địa không gian với AWS Glue, và trực quan hóa dữ liệu trong ArcGIS Pro. 
Để biết thêm các thực hành tốt nhất về lưu trữ dữ liệu địa không gian trong Amazon S3 và truy vấn với Amazon Redshift, xem [How to partition your geospatial data lake for analysis with Amazon Redshift](https://aws.amazon.com/blogs/publicsector/how-partition-geospatial-data-lake-analysis-amazon-redshift/). Mời bạn để lại phản hồi trong phần bình luận.

##  **Về tác giả**
![image14](/images/3-BlogsTranslated/29.jpg) **Jeremy Spell** là kiến trúc sư hạ tầng đám mây làm việc tại AWS Professional Services. Anh thích thiết kế và xây dựng giải pháp cho khách hàng. Trong thời gian rảnh, Jeremy thường làm món BBQ kiểu Texas và dành thời gian cho gia đình, cộng đồng nhà thờ.
![image15](/images/3-BlogsTranslated/30.jpg) **Jeff Demuth** là kiến trúc sư giải pháp gia nhập AWS từ 2016\. Anh tập trung vào cộng đồng địa không gian và đam mê hệ thống thông tin địa chất (GIS) và công nghệ. Ngoài công việc, Jeff thích du lịch, xây dựng ứng dụng IoT, và mày mò các thiết bị mới.