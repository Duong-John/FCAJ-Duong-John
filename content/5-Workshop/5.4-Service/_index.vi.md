---
title : "Dịch vụ Dữ liệu & Edge"
date : 2026-07-31 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Tổng quan
Trong phần này, chúng ta sẽ khởi tạo các dịch vụ lưu trữ dữ liệu nền tảng và thiết lập lớp mạng phân phối truy cập (Edge). Các dịch vụ này đóng vai trò là "xương sống" an toàn của toàn bộ kiến trúc (được ẩn sâu trong mạng Private) và là cổng đón nhận traffic trước khi mã nguồn ứng dụng thực sự được triển khai.

#### Nội dung triển khai:
- **Database & Cache:** Khởi tạo cơ sở dữ liệu **RDS PostgreSQL** (Single-AZ) nằm trong mạng Private DB Subnet và bộ nhớ đệm **ElastiCache Redis** trong Private App Subnet. Cả hai sẽ được bảo vệ nghiêm ngặt bởi Database Security Group.
- **Storage & Security:** Tạo **Amazon S3 Bucket** và cấu hình chính sách CORS, cho phép Frontend sử dụng phương thức PUT/GET trực tiếp thông qua Presigned URL. Đồng thời, sử dụng **AWS Secrets Manager** để gom và bảo mật các biến môi trường nhạy cảm (DATABASE_URL, REDIS_HOST, JWT_SECRET, S3_BUCKET_NAME).
- **Load Balancer & SSL:** Xin cấp phát chứng chỉ SSL/TLS miễn phí qua dịch vụ **ACM** (tại region `us-east-1`), sau đó thiết lập **ALB** cùng các **Target Group** ở khu vực chính để điều phối lưu lượng truy cập an toàn vào các container Fargate sau này.

![overview](/images/5-Workshop/5.4-Data-Edge/diagram.png)



