---
title: "Blog 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# **Các tính năng mới trong Amazon SageMaker AI tiếp tục thay đổi cách các tổ chức phát triển mô hình AI**

*Bởi Ankur Mehrotra |  Ngày 10 tháng 7 năm 2025 | liên quan [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-ai/), [Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-hyperpod/), [Amazon SageMaker JumpStart](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-jumpstart/), [Announcements](https://aws.amazon.com/blogs/machine-learning/category/post-types/announcements/)* 

Khi các mô hình trí tuệ nhân tạo (AI) ngày càng trở nên phức tạp và chuyên biệt, khả năng huấn luyện và tùy chỉnh mô hình một cách nhanh chóng chính là yếu tố quyết định giữa việc dẫn đầu hay tụt lại phía sau. Đó cũng là lý do hàng trăm nghìn khách hàng trên toàn cầu tin tưởng sử dụng [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/) — nền tảng cung cấp hạ tầng mạnh mẽ, công cụ toàn diện và quy trình làm việc được quản lý hoàn chỉnh để mở rộng và tăng tốc phát triển mô hình AI của họ. Kể từ khi ra mắt vào năm 2017, SageMaker AI đã định hình lại cách các tổ chức phát triển mô hình AI, giúp giảm thiểu độ phức tạp đồng thời tối ưu hiệu suất và khả năng mở rộng. Trong suốt quá trình đó, AWS không ngừng đổi mới — bổ sung hơn 420 tính năng mới kể từ khi ra mắt — nhằm mang đến cho khách hàng những công cụ tiên tiến nhất để xây dựng, huấn luyện và triển khai mô hình AI một cách nhanh chóng, linh hoạt và hiệu quả. Hôm nay, chúng tôi tiếp tục hành trình đó với việc giới thiệu những cải tiến mới nhất của SageMaker AI, được thiết kế để đẩy nhanh quá trình phát triển và huấn luyện mô hình, giúp các tổ chức rút ngắn thời gian đổi mới và khai thác tối đa tiềm năng của AI.

## **Amazon SageMaker HyperPod: Hạ tầng lý tưởng cho việc phát triển các mô hình trí tuệ nhân tạo**

AWS ra mắt [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) vào năm 2023 nhằm giảm độ phức tạp và tối đa hóa hiệu năng cũng như hiệu quả khi xây dựng mô hình AI. Với SageMaker HyperPod, bạn có thể nhanh chóng mở rộng phát triển mô hình AI sinh (generative) trên hàng nghìn bộ gia tốc AI và giảm tới 40% chi phí huấn luyện và tinh chỉnh mô hình nền tảng (FM). Nhiều mô hình hàng đầu hiện nay được huấn luyện trên SageMaker HyperPod, bao gồm mô hình từ Hugging Face, Luma AI, Perplexity AI, Salesforce, Thomson Reuters, Writer và Amazon. Bằng cách huấn luyện các FM [Amazon Nova](https://aws.amazon.com/ai/generative-ai/nova/) trên SageMaker HyperPod, Amazon đã tiết kiệm được hàng tháng công việc và nâng mức sử dụng tài nguyên tính toán lên hơn 90%.

*[Amazon Trains Nova Foundation Models at Scale with SageMaker HyperPod | Amazon Web Services](https://youtu.be/aS1EU_kkGcI)*

Để tối ưu quy trình và tăng tốc phát triển, triển khai mô hình, một giao diện dòng lệnh (CLI) và bộ SDK mới cung cấp một giao diện thống nhất, nhất quán, đơn giản hóa quản lý hạ tầng, hợp nhất việc gửi tác vụ giữa huấn luyện và suy luận, và hỗ trợ cả quy trình theo “recipe” lẫn tùy biến với giám sát và điều khiển tích hợp. Hôm nay, chúng tôi cũng bổ sung hai khả năng cho SageMaker HyperPod giúp bạn giảm chi phí huấn luyện và tăng tốc phát triển mô hình AI.

## **Giảm thời gian xử lý sự cố hiệu năng từ vài ngày xuống vài phút với khả năng quan sát của SageMaker HyperPod**

Để đưa các đổi mới AI ra thị trường nhanh nhất, tổ chức cần khả năng quan sát xuyên suốt các tác vụ phát triển mô hình AI và tài nguyên tính toán nhằm tối ưu hiệu suất huấn luyện và phát hiện, khắc phục gián đoạn hoặc nút thắt hiệu năng sớm nhất. Ví dụ, để điều tra xem một tác vụ huấn luyện hay tinh chỉnh thất bại có do lỗi phần cứng hay không, các nhà khoa học dữ liệu và kỹ sư ML muốn nhanh chóng lọc và xem dữ liệu giám sát của các GPU cụ thể đã chạy tác vụ, thay vì phải duyệt thủ công tài nguyên phần cứng của cả cụm để xác lập tương quan giữa lỗi tác vụ và sự cố phần cứng.

[Khả năng quan sát mới trong SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/accelerate-foundation-model-development-with-one-click-observability-in-amazon-sagemaker-hyperpod/) thay đổi cách bạn giám sát và tối ưu khối lượng công việc phát triển mô hình. Thông qua một bảng điều khiển hợp nhất được cấu hình sẵn trong [Amazon Managed Grafana](https://aws.amazon.com/grafana/), với dữ liệu giám sát tự động được gửi tới một workspace [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/), bạn có thể xem các chỉ số hiệu năng tác vụ AI sinh, mức sử dụng tài nguyên và sức khỏe cụm trong một màn hình duy nhất. Nhóm có thể nhanh chóng phát hiện nút thắt, ngăn chặn trì hoãn tốn kém và tối ưu tài nguyên tính toán. Bạn có thể định nghĩa cảnh báo tự động, chỉ định các chỉ số và sự kiện theo trường hợp sử dụng, và xuất chúng lên bảng điều khiển hợp nhất chỉ với vài cú nhấp.

Bằng cách rút ngắn thời gian khắc phục sự cố từ ngày xuống phút, khả năng này giúp bạn tăng tốc đưa vào sản xuất và tối đa hóa lợi nhuận từ đầu tư AI.

![image1](/images/3-BlogsTranslated/01.jpg)

DatologyAI xây dựng công cụ để tự động chọn dữ liệu tốt nhất để huấn luyện mô hình học sâu.

*“Chúng tôi háo hức sử dụng giải pháp quan sát một-cú-nhấp của Amazon SageMaker HyperPod. Các nhân sự cấp cao của chúng tôi cần hiểu sâu cách chúng tôi sử dụng tài nguyên GPU. Các bảng điều khiển Grafana dựng sẵn sẽ mang đến đúng những gì chúng tôi cần, với khả năng quan sát tức thì các chỉ số quan trọng \- từ mức sử dụng GPU theo tác vụ đến hiệu năng hệ thống tệp (FSx for Lustre) \- mà không cần tự vận hành hạ tầng giám sát. Là người đánh giá cao sức mạnh của Prometheus Query Language, tôi thích việc có thể tự viết truy vấn và phân tích các chỉ số tùy chỉnh mà không phải lo về hạ tầng.”*

\- Josh Wills, Thành viên Đội ngũ Kỹ thuật tại DatologyAI

![image2](/images/3-BlogsTranslated/02.jpg)

Articul8 giúp doanh nghiệp xây dựng các ứng dụng AI sinh cho doanh nghiệp ở mức độ tinh vi.

*“Với khả năng quan sát của SageMaker HyperPod, giờ đây chúng tôi có thể triển khai hệ thống thu thập và trực quan hóa chỉ số trong một cú nhấp, tiết kiệm cho đội ngũ nhiều ngày thiết lập thủ công và tăng cường quy trình, insight quan sát cụm. Các nhà khoa học dữ liệu có thể nhanh chóng theo dõi các chỉ số hiệu năng tác vụ, như độ trễ, và xác định vấn đề phần cứng mà không cần cấu hình thủ công. Khả năng quan sát của HyperPod sẽ tinh gọn quy trình phát triển mô hình nền tảng, cho phép chúng tôi tập trung vào sứ mệnh mang đến đổi mới AI đáng tin cậy, dễ tiếp cận cho khách hàng.”*  
\- Renato Nascimento, trưởng bộ phận công nghệ tại Articul8

## **Triển khai các mô hình Amazon SageMaker JumpStart trên SageMaker HyperPod để suy luận nhanh, mở rộng**

Sau khi phát triển mô hình AI sinh trên SageMaker HyperPod, nhiều khách hàng nhập các mô hình này vào [Amazon Bedrock](https://aws.amazon.com/bedrock/), dịch vụ được quản lý toàn phần để xây dựng và mở rộng ứng dụng AI sinh. Tuy nhiên, một số khách hàng muốn dùng tài nguyên tính toán của SageMaker HyperPod để tăng tốc đánh giá và đưa mô hình vào sản xuất nhanh hơn.

Giờ đây, bạn có thể [triển khai các mô hình open-weights](https://aws.amazon.com/blogs/machine-learning/amazon-sagemaker-hyperpod-launches-model-deployments-to-accelerate-the-generative-ai-model-development-lifecycle/) từ Amazon SageMaker JumpStart, cũng như các mô hình tùy chỉnh đã tinh chỉnh, trên SageMaker HyperPod chỉ trong vài phút mà không cần thiết lập hạ tầng thủ công. Nhà khoa học dữ liệu có thể chạy suy luận trên các mô hình JumpStart chỉ với một cú nhấp, đơn giản hóa và tăng tốc việc đánh giá mô hình. Quy trình cấp phát một lần, đơn giản này giảm thiết lập thủ công, mang lại môi trường suy luận đáng tin cậy và có khả năng mở rộng với nỗ lực ít nhất. Việc tải xuống các mô hình lớn được rút ngắn từ hàng giờ xuống còn vài phút, tăng tốc triển khai và rút ngắn thời gian ra thị trường.

![image3](/images/3-BlogsTranslated/03.jpg)

H.AI tồn tại để phá vỡ giới hạn siêu trí tuệ với AI hướng tác vụ (agentic AI).

*“Với Amazon SageMaker HyperPod, chúng tôi dùng  hạ tầng tính toán hiệu năng cao để xây dựng và triển khai các mô hình nền tảng đứng sau nền tảng AI hướng tác vụ của mình. Việc chuyển đổi liền mạch từ huấn luyện sang suy luận đã tinh gọn quy trình, rút ngắn thời gian vào sản xuất và mang lại hiệu năng ổn định trong môi trường thực. HyperPod giúp chúng tôi đi từ thử nghiệm đến tác động thực tế nhanh chóng và hiệu quả hơn.”*

\- Laurent Sifre, Đồng sáng lập & CTO tại H.AI

## **Truy cập liền mạch tài nguyên tính toán mạnh mẽ của SageMaker AI từ môi trường phát triển cục bộ**

Hiện nay, nhiều khách hàng chọn các môi trường phát triển tích hợp (IDE) được quản lý toàn phần trong SageMaker AI để phát triển mô hình, gồm JupyterLab, Code Editor dựa trên Code-OSS, và RStudio. Dù các IDE này mang lại thiết lập an toàn và hiệu quả, một số nhà phát triển thích dùng IDE cục bộ trên máy cá nhân vì khả năng gỡ lỗi và tùy biến sâu. Tuy nhiên, khách hàng dùng IDE cục bộ như Visual Studio Code trước đây không thể dễ dàng chạy các tác vụ phát triển mô hình trên SageMaker AI.

Với [các kết nối từ xa mới tới SageMaker AI](https://aws.amazon.com/blogs/machine-learning/supercharge-your-ai-workflows-by-connecting-to-sagemaker-studio-from-visual-studio-code), nhà phát triển và nhà khoa học dữ liệu có thể nhanh chóng, liền mạch kết nối tới SageMaker AI từ VS Code cục bộ, vẫn giữ quyền truy cập công cụ tùy chỉnh và quy trình quen thuộc giúp họ làm việc hiệu quả nhất. Nhà phát triển có thể xây dựng và huấn luyện mô hình AI bằng IDE cục bộ trong khi SageMaker AI quản lý thực thi từ xa, nên bạn có thể làm việc trong môi trường ưa thích đồng thời hưởng lợi từ hiệu năng, khả năng mở rộng và bảo mật của SageMaker AI. Giờ đây bạn có thể chọn IDE ưa thích \- dù là IDE đám mây được quản lý toàn phần hay VS Code \- để tăng tốc phát triển mô hình AI bằng hạ tầng mạnh mẽ và khả năng mở rộng liền mạch của SageMaker AI.

![image4](/images/3-BlogsTranslated/04.jpg)

CyberArk là công ty dẫn đầu về Bảo mật Danh tính, cung cấp cách tiếp cận toàn diện xoay quanh kiểm soát đặc quyền để bảo vệ trước các mối đe dọa mạng tiên tiến.

*“Với kết nối từ xa tới SageMaker AI, các nhà khoa học dữ liệu của chúng tôi có sự linh hoạt chọn IDE giúp họ năng suất nhất. Các đội có thể tận dụng thiết lập cục bộ đã tùy chỉnh trong khi tiếp cận hạ tầng và kiểm soát bảo mật của SageMaker AI. Là công ty đặt an ninh lên hàng đầu, điều này cực kỳ quan trọng vì đảm bảo dữ liệu nhạy cảm luôn được bảo vệ, đồng thời cho phép đội ngũ cộng tác an toàn và tăng năng suất.”*

- Nir Feldman, Phó Chủ tịch cấp cao Kỹ thuật tại CyberArk

## **Xây dựng mô hình và ứng dụng AI sinh nhanh hơn với MLflow 3.0 được quản lý toàn phần**

Khi khách hàng trong nhiều ngành tăng tốc phát triển AI sinh, họ cần khả năng theo dõi thí nghiệm, quan sát hành vi và đánh giá hiệu năng của mô hình và ứng dụng AI. Khách hàng như Cisco, SonRai và Xometry đã sử dụng MLflow được quản lý trên SageMaker AI để quản lý hiệu quả thí nghiệm mô hình ML ở quy mô lớn. Việc giới thiệu MLflow 3.0 được quản lý toàn phần trên SageMaker AI giúp việc theo dõi thí nghiệm, giám sát tiến trình huấn luyện và có insight sâu hơn về hành vi của mô hình và ứng dụng AI chỉ với một công cụ duy nhất, hỗ trợ bạn tăng tốc phát triển AI sinh.

## 

## 

## **Kết luận**

Trong bài viết này, chúng tôi đã chia sẻ một số đổi mới trong SageMaker AI để tăng tốc cách bạn xây dựng và huấn luyện mô hình AI.

Để tìm hiểu thêm về các tính năng mới, SageMaker AI, và cách các công ty sử dụng dịch vụ này, hãy tham khảo các tài nguyên sau:

* [Tăng tốc phát triển mô hình nền tảng với khả năng quan sát một-cú-nhấp trong Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/accelerate-foundation-model-development-with-one-click-observability-in-amazon-sagemaker-hyperpod)  
* [Tăng tốc quy trình AI của bạn bằng cách kết nối tới SageMaker Studio từ Visual Studio Code](https://aws.amazon.com/blogs/machine-learning/supercharge-your-ai-workflows-by-connecting-to-sagemaker-studio-from-visual-studio-code)  
* [Tăng tốc phát triển AI sinh với MLflow 3.0 được quản lý toàn phần trên Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/accelerating-generative-ai-development-with-fully-managed-mlflow-3-0-on-amazon-sagemaker-ai/)  
* [Amazon SageMaker HyperPod ra mắt triển khai mô hình để tăng tốc vòng đời phát triển mô hình AI sinh](https://aws.amazon.com/blogs/machine-learning/amazon-sagemaker-hyperpod-launches-model-deployments-to-accelerate-the-generative-ai-model-development-lifecycle/)  
* [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/)  
* [Khách hàng của Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/customers/)

## **Về tác giả**

**Ankur Mehrotra** gia nhập Amazon từ năm 2008 và hiện là Tổng Giám đốc Amazon SageMaker AI. Trước SageMaker AI, anh đã tham gia xây dựng hệ thống quảng cáo và công nghệ định giá tự động của Amazon.com.

![image5](/images/3-BlogsTranslated/05.png)(\n)