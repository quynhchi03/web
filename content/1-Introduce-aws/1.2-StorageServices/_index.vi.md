---
title : "Dịch vụ lưu trữ"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1.1 </b> "
---

## Giới thiệu dịch vụ lưu trữ AWS
Amazon S3 là dịch vụ lưu trữ đối tượng có khả năng mở rộng được thiết kế để lưu trữ và truy xuất mọi lượng dữ liệu từ mọi nơi trên web. Nó có độ bền cao, an toàn và tiết kiệm chi phí.
S3 cung cấp các tính năng như lập phiên bản, mã hóa, kiểm soát truy cập và quản lý vòng đời để quản lý dữ liệu một cách hiệu quả.

Nó thường được sử dụng cho nhiều trường hợp sử dụng, bao gồm sao lưu và khôi phục, lưu trữ dữ liệu, phân phối nội dung và lưu trữ các trang web tĩnh.

![S3](../../images/1.2-StorageService/s3.png)
#### Lớp lưu trữ đối tượng(Object Storage Classes):

**Amazon S3 Standard (S3 Standard):** S3 Standard cung cấp khả năng lưu trữ đối tượng có độ bền cao, tính khả dụng và hiệu suất cao cho dữ liệu được truy cập thường xuyên. Vì mang lại độ trễ thấp và thông lượng cao nên S3 Standard phù hợp với nhiều trường hợp sử dụng khác nhau, bao gồm ứng dụng đám mây, trang web động, phân phối nội dung, ứng dụng di động và trò chơi cũng như phân tích dữ liệu lớn. 

Các tính năng chính:
+ Lưu trữ mục đích chung cho dữ liệu được truy cập thường xuyên
+ Độ trễ thấp và hiệu suất thông lượng cao
+ Được thiết kế để cung cấp mức độ khả dụng 99,99% với SLA khả dụng là 99,9%

**Amazon S3 Intelligent-Tiering (S3 Intelligent-Tiering):** thường được viết tắt là S3 Intelligence-Tiering, là lớp lưu trữ được Amazon Web Services (AWS) giới thiệu cho Dịch vụ lưu trữ đơn giản (S3) của họ. Nó được thiết kế để tự động tối ưu hóa chi phí lưu trữ bằng cách di chuyển dữ liệu giữa hai tầng truy cập: truy cập thường xuyên và truy cập không thường xuyên, dựa trên mô hình sử dụng.

Cách thức hoạt động của Phân bậc thông minh S3 (S3 Intelligent-Tiering):

+ Phân bậc tự động (Automatic Tiering): S3 Phân bậc thông minh tự động giám sát các kiểu truy cập dữ liệu của bạn và di chuyển các đối tượng giữa hai tầng truy cập: truy cập thường xuyên và truy cập không thường xuyên. Dữ liệu được truy cập thường xuyên vẫn ở cấp truy cập thường xuyên, trong khi dữ liệu không được truy cập trong một khoảng thời gian sẽ được chuyển sang cấp truy cập không thường xuyên.

+ Tối ưu hóa chi phí(Cost Optimization): Bằng cách tự động di chuyển dữ liệu giữa các tầng truy cập, S3 Phân bậc thông minh giúp tối ưu hóa chi phí lưu trữ. Bạn không cần quản lý thủ công việc di chuyển dữ liệu giữa các tầng, giảm chi phí vận hành.

+ No Retrieval Fees: Unlike some other storage classes in S3, S3 Intelligent-Tiering does not incur retrieval fees when accessing data from the infrequent access tier. This makes it particularly cost-effective for data with unpredictable access patterns.

+ Durability and Availability: S3 Intelligent-Tiering provides the same high durability and availability as other S3 storage classes, ensuring that your data is protected against hardware failures and is accessible when needed.

+ Monitoring and Analytics: AWS provides tools for monitoring and analyzing the access patterns of your data stored in S3 Intelligent-Tiering. This allows you to gain insights into your data usage and make informed decisions about storage optimization.

#### Use S3 in which situation?
+ Data Backup and Archiving: S3 provides a reliable and cost-effective solution for storing backups and archives of data. Its high durability ensures that data remains safe over extended periods, making it ideal for long-term storage requirements.

+ Static Website Hosting: S3 can host static websites by storing HTML, CSS, JavaScript, and other web assets. It integrates seamlessly with other AWS services like Amazon Route 53 for DNS routing and Amazon CloudFront for content delivery, enabling fast and scalable website hosting.

+ Content Distribution: S3 combined with Amazon CloudFront allows you to distribute content globally with low latency and high transfer speeds. This is useful for delivering large files, streaming media, or website assets to users worldwide.

+ Application Data Storage: Many applications use S3 as a central storage repository for various types of data, such as user-generated content, media files, application logs, and configuration files. S3's scalability and reliability make it suitable for storing large volumes of diverse data types.

+ Big Data Analytics: S3 serves as a data lake for storing vast amounts of structured and unstructured data that can be analyzed using AWS analytics services like Amazon Athena, Amazon Redshift Spectrum, or AWS Glue. Data stored in S3 can be queried directly without the need for data movement.

+ Disaster Recovery: S3 can be part of a disaster recovery strategy, where critical data backups are stored in S3 buckets across different AWS regions. In the event of a disaster, data can be quickly restored from S3 to maintain business continuity.

+ Data Warehousing: S3 can act as a staging area for data ingested into data warehouses like Amazon Redshift or Amazon Athena. Data is first loaded into S3 and then processed by the analytics services, allowing for scalable and cost-effective data storage.

+ Mobile and IoT Applications: S3 is often used as a storage backend for mobile and IoT applications to store user-generated content, sensor data, and application logs. Its scalability and compatibility with AWS SDKs make it easy to integrate with various application platforms.

### 2. Amazon EBS (Elastic Block Store):
Amazon Elastic Block Store (EBS) is a block-level storage service provided by Amazon Web Services (AWS) that is designed for use with Amazon EC2 (Elastic Compute Cloud) instances. 

**Block-Level Storage:**
+ Amazon EBS provides block-level storage volumes that are similar to physical hard drives or SSDs, allowing users to create and attach storage volumes to EC2 instances.
+ These volumes appear as raw block devices to the EC2 instances and can be formatted and mounted like any other block storage device.

**Persistence and Durability:**
+ EBS volumes are designed for durability and reliability. Data stored on EBS volumes is replicated within the same Availability Zone to ensure data durability.
+ EBS volumes are persistent, meaning that data persists even after the associated EC2 instance is terminated. Users can detach EBS volumes from one EC2 instance and attach them to another without losing data.

**High Performance:**
+ EBS volumes offer high-performance storage options, including SSD-backed volumes (EBS-SSD) and magnetic volumes (EBS-HDD), to meet the performance requirements of different workloads.
+ SSD-backed volumes provide low-latency and high IOPS (Input/Output Operations Per Second) for performance-sensitive applications, while magnetic volumes offer cost-effective storage for less demanding workloads.

**Snapshot and Backup:**
+ EBS volumes support snapshots, which are point-in-time backups of the volume data stored in Amazon S3. Users can create snapshots of EBS volumes manually or automatically using scheduled snapshots.
+ Snapshots are incremental, meaning that only the changed blocks since the last snapshot are stored, which helps reduce storage costs and backup times.

**Encryption and Security:**
+ EBS volumes support encryption using AWS Key Management Service (KMS), allowing users to encrypt data at rest to meet compliance and security requirements.
+ Users can also specify encryption settings when creating new EBS volumes or encrypt existing volumes using snapshots.

**Scalability and Flexibility:**
+ EBS volumes can be resized dynamically without any downtime, allowing users to scale storage capacity based on changing workload requirements.
+ Users can choose from a range of volume types and sizes to meet the performance and capacity needs of their applications.

**Integration with AWS Services**
+ EBS volumes can be integrated with other AWS services such as Amazon EC2, Amazon RDS (Relational Database Service), and AWS Lambda to provide storage for various types of applications and workloads.
#### Use EBS in which situation?
+ Amazon Elastic Block Store (EBS) is used in various situations where persistent and scalable block storage is required for applications running on single Amazon EC2 instance
### 3. Amazon EFS (Elastic File System)

Amazon EFS is a scalable and fully managed file storage service designed to provide scalable and shared access to files from multiple EC2 instances.
It supports NFS (Network File System) protocol and can be seamlessly integrated with existing applications and workflows.

EFS is suitable for use cases such as content management, media processing, software development, and data analytics that require shared file storage.
#### Use EFS in which situation?

Amazon EFS is commonly used in situations where multiple EC2 instances need shared access to a common file system. It provides a centralized and scalable storage solution for applications that require shared file storage

### 4. Amazon FSx (File Storage)

Amazon FSx offers fully managed file storage services optimized for specific use cases, including Amazon FSx for Windows File Server and Amazon FSx for Lustre.
FSx for Windows File Server provides fully managed, highly available Windows file shares, while FSx for Lustre delivers high-performance file systems for compute-intensive workloads.

FSx is suitable for applications that require Windows-compatible file storage or high-performance file systems for compute-intensive workloads such as machine learning and simulation.
#### Use FSx in which situation?
+ Amazon FSx for Windows File Server is used in situations where users need a fully managed Windows-compatible file system with support for SMB (Server Message Block) protocol.
+ It provides a scalable and fully managed Windows file system that is accessible from Windows, Linux, and macOS clients, making it suitable for file sharing and collaboration across different platforms.