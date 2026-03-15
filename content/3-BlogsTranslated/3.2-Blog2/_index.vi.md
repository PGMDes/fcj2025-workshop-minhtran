---
title: "Blog 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# **Nâng cao độ chính xác dự báo thời tiết bằng các phiên bản đồ họa chuyên sâu của Amazon AppStream 2.0**

*Bởi Rayette Toles-Abdullah, Austin Park, và Chris Quarcoo | Ngày 13 tháng 5 năm 2025 | liên quan [Amazon AppStream 2.0](https://aws.amazon.com/blogs/publicsector/category/desktop-app-streaming/amazon-appstream-2-0/), [Best Practices](https://aws.amazon.com/blogs/publicsector/category/post-types/best-practices/), [Customer Solutions](https://aws.amazon.com/blogs/publicsector/category/post-types/customer-solutions/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/)*

![image1](/images/3-BlogsTranslated/06.png)

Khả năng truy cập ứng dụng và dữ liệu từ bất cứ đâu trên bất kỳ thiết bị nào ngày càng quan trọng đối với lực lượng lao động làm việc từ xa, kết nối hạn chế, và phân tán. Các nhà nghiên cứu thực địa và nhà khí tượng học trên toàn cầu phụ thuộc vào việc thu nhận dữ liệu theo thời gian thực cho các khả năng thời tiết thiết yếu.

Hệ thống Xử lý Tương tác Thời tiết Nâng cao (AWIPS) là một hệ thống dự báo và hiển thị thời tiết được sử dụng bởi Cơ quan Thời tiết Quốc gia Hoa Kỳ (NWS) và các cơ quan khí tượng trên toàn thế giới. Hệ thống cho phép các nhà khí tượng giám sát, phân tích và dự đoán các mô hình thời tiết với độ chính xác cao hơn, mang lại dự báo tốt hơn và cảnh báo hiệu quả hơn nhằm giúp bảo vệ tính mạng và tài sản. AWIPS tích hợp dữ liệu từ nhiều nguồn như vệ tinh, radar và bóng thám không. Common AWIPS Visualization Environment (CAVE) là ứng dụng phía khách mà các nhà dự báo dùng để tương tác với hệ thống AWIPS. CAVE nhận dữ liệu đã xử lý từ các máy chủ AWIPS và cung cấp các công cụ trực quan hóa giúp các nhà khí tượng lập dự báo, phát hành cảnh báo, và trực quan hóa dữ liệu thời tiết.

Trong bài viết này, chúng tôi sẽ hướng dẫn bạn cách truyền phát ứng dụng Common AWIPS Visualization Environment (CAVE) bằng [Amazon AppStream 2.0](https://aws.amazon.com/pm/appstream2/)\-một dịch vụ truyền phát ứng dụng được quản lý, cho phép người dùng truyền phát các ứng dụng desktop từ Amazon Web Services (AWS) đến bất kỳ thiết bị nào mà không cần phần cứng hay phần mềm bổ sung.

## **Lợi ích khi chạy các ứng dụng đồ họa chuyên sâu bằng Amazon AppStream 2.0**

AppStream 2.0 mang lại nhiều lợi ích. Với dịch vụ truyền phát này:

* Người dùng có thể truy cập các ứng dụng desktop từ bất kỳ thiết bị được hỗ trợ nào, bao gồm laptop, máy tính để bàn, máy tính bảng và điện thoại. Điều này mang lại sự linh hoạt và tính di động, giúp nhân viên duy trì năng suất dù ở văn phòng, làm việc tại nhà hay đang di chuyển.  
* Bạn có thể dễ dàng tăng hoặc giảm dung lượng GPU theo nhu cầu. Điều này giúp tối ưu chi phí bằng cách chỉ trả tiền cho những gì bạn sử dụng, loại bỏ nhu cầu duy trì phần cứng đắt tiền có thể bị nhàn rỗi trong giờ thấp điểm.  
* Bạn không cần cấp thừa nguồn lực GPU, điều đặc biệt giá trị đối với các tổ chức có khối lượng công việc biến động hoặc theo mùa.  
* Người dùng có thể truy cập các ứng dụng tăng tốc GPU từ bất kỳ thiết bị nào, bao gồm thiết bị di động. Điều này mang lại sự linh hoạt hơn so với việc gắn ứng dụng với các desktop cụ thể, và cung cấp hiệu năng nhất quán bất kể khả năng của thiết bị người dùng cuối.  
* AppStream 2.0 xử lý các phức tạp của việc quản lý driver GPU, các đội máy (fleet) hỗ trợ GPU và các stack ứng dụng tối ưu cho GPU. Điều này giảm gánh nặng quản trị cho đội ngũ IT, giúp họ tập trung vào các sáng kiến chiến lược thay vì bảo trì định kỳ và xử lý sự cố.  
* GPU được cung cấp theo mô hình trả tiền theo mức sử dụng (pay-as-you-go) trong AppStream 2.0, loại bỏ chi phí đầu tư ban đầu cao để mua và bảo trì máy chủ GPU vật lý. Điều này giúp giải pháp trở nên phải chăng hơn đối với nhiều tổ chức, đặc biệt là những đơn vị mới bắt đầu hoặc muốn mở rộng năng lực đồ họa mà không cần chi tiêu vốn lớn.  
* AppStream 2.0 cung cấp các loại phiên bản tối ưu cho khối lượng công việc đồ họa như Graphics G4dn và Graphics G5 sử dụng GPU NVIDIA. Điều này mang lại hiệu năng cao cho các tác vụ như mô hình 3D và biên tập video, đồng thời cho phép bạn chọn loại phiên bản phù hợp nhất với yêu cầu ứng dụng và nhu cầu người dùng cụ thể.  
* Khối lượng công việc GPU và dữ liệu của bạn không bao giờ lưu trú trên thiết bị người dùng cuối và được cô lập trong Đám mây AWS. Điều này tăng cường bảo mật và tuân thủ cho các ứng dụng nhạy cảm, đồng thời cung cấp khả năng kiểm soát tập trung đối với quyền truy cập dữ liệu và giảm rủi ro mất mát tài sản trí tuệ do thiết bị cục bộ bị xâm phạm.

![image2](/images/3-BlogsTranslated/07.png) 
Hình 1\. Trực quan hóa AWIPS CAVE về Bão Lee ngày 13/9/2023 sử dụng Amazon AppStream 2.0.

## **Khám phá giải pháp AWIPS**

Trạm làm việc AWIPS CAVE là giao diện chính mà các nhà dự báo sử dụng. AWIPS CAVE có các yêu cầu hệ thống sau:

* Thiết bị tương thích OpenGL 2.0  
* Tối thiểu 4GB RAM  
* Tối thiểu 2GB dung lượng đĩa cho bộ nhớ đệm  
* Card đồ họa NVIDIA  
* Driver NVIDIA mới nhất

Để cấu hình ứng dụng AWIPS cho Amazon AppStream 2.0, bạn sẽ thực hiện các bước sau:

### **Tạo Image dựa trên Linux**

Trước tiên, chúng ta sẽ chuẩn bị môi trường Linux nền tảng và cài đặt AWIPS CAVE cùng các phụ thuộc của nó. Điều này tạo nền tảng cho ứng dụng truyền phát của chúng ta.

![image3](/images/3-BlogsTranslated/08.png)

### **Tạo Manifest Tối ưu hóa Ứng dụng**

Amazon AppStream 2.0 sử dụng các tệp manifest để tối ưu hiệu năng truyền phát ứng dụng bằng cách nạp trước các tệp cần thiết. Script này giúp xác định tất cả các tệp mà CAVE cần trong thời gian chạy.

![image4](/images/3-BlogsTranslated/09.png)

### **Thêm Ứng dụng vào Danh mục Amazon AppStream**

Đăng ký CAVE trong danh mục ứng dụng Amazon AppStream, xác định đường dẫn khởi chạy, tên hiển thị và tệp manifest tối ưu hóa mà chúng ta đã tạo.

![image5](/images/3-BlogsTranslated/10.png)

### **Cấu hình Fleet**

Tạo một fleet để quản lý các phiên bản sẽ chạy ứng dụng truyền phát của bạn. Chọn giữa cấu hình on-demand (tiết kiệm chi phí) hoặc always-on (sẵn sàng tức thì).

* Khuyến nghị chọn Graphics G4dn (stream.graphics.g4dn.xlarge) hoặc Graphics Pro (stream.graphics-pro.4xlarge)  
* Chọn loại fleet “On-demand”  
* Đặt các giới hạn dung lượng mong muốn

### 

### 

### 

### **Tạo Image**

Tạo image Amazon AppStream cuối cùng sẽ được dùng để khởi chạy các phiên truyền phát. Quá trình này chụp lại tất cả ứng dụng và cấu hình đã cài đặt.

![image6](/images/3-BlogsTranslated/11.png)

### **Cấu hình Xác thực Người dùng**

Chọn giữa việc quản lý người dùng trực tiếp trong Amazon AppStream hoặc tích hợp với nhà cung cấp danh tính hiện có của bạn.

* Cấu hình xác thực Amazon Cognito User Pool  
* Tích hợp Môi trường Amazon AppStream với AWS Identity Center.

Hình sau mô tả kiến trúc cấp cao của giải pháp.

![image7](/images/3-BlogsTranslated/12.png)

Hình 2\. Sơ đồ kiến trúc của giải pháp mô tả trong bài. Các thành phần chính của giải pháp gồm Amazon AppStream 2.0, Amazon S3, Amazon EFS, Amazon Aurora, và Amazon EC2.

## **Các trường hợp sử dụng AWIPS ngoài hiện trường**

Các Trung tâm Dự báo Sông (RFC) của NWS sử dụng AWIPS CAVE để giám sát và dự đoán mực nước sông, suối, phát hành cảnh báo lũ, và cung cấp thông tin về nguồn nước và điều kiện hạn hán. Các Văn phòng Dự báo Thời tiết (WFO) dựa vào AWIPS CAVE để cung cấp cho công chúng các dự báo thời tiết địa phương, cảnh báo và khuyến cáo. Các văn phòng này cũng sử dụng AWIPS CAVE để phối hợp với các WFO khác, các cơ quan liên bang và tiểu bang, cũng như các đối tác khu vực tư nhân. Trung tâm Bão Quốc gia NWS (NHC) sử dụng AWIPS CAVE để theo dõi và dự báo xoáy thuận nhiệt đới, bao gồm bão và áp thấp nhiệt đới. AWIPS CAVE hỗ trợ NHC trong việc cung cấp thông tin kịp thời và chính xác cho công chúng, các quan chức quản lý khẩn cấp và các bên liên quan khác. Ngoài ra, một số trường đại học và viện nghiên cứu tập trung vào khí tượng và khoa học khí quyển cũng sử dụng AWIPS CAVE cho mục đích nghiên cứu, giảng dạy và đào tạo.

## **Kết luận**

Việc tích hợp AWIPS CAVE với Amazon AppStream 2.0 đại diện cho một bước tiến đáng kể trong công nghệ và khả năng tiếp cận của dự báo thời tiết. Giải pháp này đáp ứng nhu cầu ngày càng tăng về truy cập từ xa tới các ứng dụng trọng yếu trong lĩnh vực khí tượng, đồng thời mang lại nhiều lợi ích về tính linh hoạt, hiệu quả chi phí và hiệu năng.

Bằng cách tận dụng sức mạnh của điện toán đám mây và tăng tốc GPU, các nhà khí tượng và nhà nghiên cứu hiện có thể truy cập các công cụ phân tích thời tiết tinh vi từ bất kỳ đâu, trên bất kỳ thiết bị nào. Điều này không chỉ nâng cao khả năng cung cấp các dự báo chính xác và kịp thời mà còn cải thiện hiệu quả tổng thể của các dịch vụ thời tiết.

Khi chúng ta tiếp tục đối mặt với các mô hình thời tiết ngày càng phức tạp và thách thức khí hậu, những đổi mới công nghệ như vậy sẽ đóng vai trò then chốt trong việc hỗ trợ công việc của các nhà khí tượng và cuối cùng là góp phần vào an toàn, sẵn sàng của cộng đồng.

**Về tác giả**
| :---- | :---- |
| ![image8](/images/3-BlogsTranslated/13.jpg) | **Rayette Toles-Abdullah** Rayette là kiến trúc sư giải pháp chính trong đội Worldwide Public Sector Federal Civilian tại AWS. Rayette là một chuyên gia công nghệ với hơn 23 năm kinh nghiệm, chuyên về tích hợp hệ thống, hiện đại hóa ứng dụng, và triển khai các giải pháp công nghệ tác động cao để giải quyết nhu cầu kinh doanh và nhiệm vụ. |
| ![image9](/images/3-BlogsTranslated/14.png) | **Austin Park** Austin là kiến trúc sư giải pháp trong đội Worldwide Public Sector Federal Civilian tại AWS. Austin là một chuyên gia công nghệ với hơn 2 năm kinh nghiệm, chuyên về hệ thống lưu trữ. Austin đam mê hỗ trợ khách hàng AWS trên hành trình lên đám mây. |
| ![image10](/images/3-BlogsTranslated/15.jpg) | **Chris Quarcoo** Chris là kiến trúc sư giải pháp trong đội Worldwide Public Sector tại AWS, với hơn 4 năm kinh nghiệm trong ngành CNTT. Chuyên về vận hành đám mây và công nghệ container, anh thiết kế và triển khai các giải pháp đám mây cho các tổ chức chính phủ và khu vực công. Chris tận dụng công nghệ AWS để giúp khách hàng hiện đại hóa hạ tầng CNTT, nâng cao chất lượng dịch vụ, và đạt được các mục tiêu nhiệm vụ trọng yếu trong khu vực công. |