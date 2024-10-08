# 1. Introduction

### 1.1 Hadoop Goals:

>This section defines the main goals of Hadoop, including `scalable` and `reliable data storage`, powerful data processing, and efficient visualization. It also acknowledges the challenges of `slow storage`, unreliable computers, and difficulties in `distributed parallel programming`.
## Mục tiêu của Hadoop 
• Mục tiêu chính 
	• Lưu trữ dữ liệu khả mở, tin cậy 
	• Powerful data processing 
	• Efficient visualization 
• Với thách thức 
	• Thiết bị lưu trữ tốc độ chậm, máy tính thiếu tin cậy, lập trình song song phân tán không dễ dàng
### 1.2 Introducing Apache Hadoop: 
>This section highlights Hadoop's features like `cost-effective` storage and processing, `distributed processing` with the MapReduce model, `scalability` through scale-out architecture, fault-tolerance on commodity hardware, and its inspiration from `Google's data architecture.`
### 1.3 Key Hadoop Components: 
>This section introduces the `three main components` of Hadoop

- Data storage: `HDFS`
- Data processing: `MapReduce`
- System utilities: `Hadoop Common` (hỗ trợ các thành phần của Hadoop), `Hadoop YARN` (quản lý tài nguyên và lập lịch)
### 1.4 Hadoop: giải quyết bài toán khả mở
>This section explains how Hadoop's `distributed design`, `node-based architecture`, and `scale-out` capabilities address scalability issues in big data.

• Thiết kế hướng “phân tán” ngay từ đầu 
	• Hadoop mặc định thiết kế để triển khai trên cụm máy chủ 
• Các máy chủ tham gia vào cụm được gọi là các Nodes 
	• Mỗi node tham gia vào cả 2 vai trò lưu trữ và tính toán 
• Hadoop mở rộng bằng kỹ thuật scale-out 
	• Có thể tăng cụm Hadoop lên hàng chục ngàn nodes
### 1.5 Hadoop: giải quyết bài toán chịu lỗi: 
>This section explains how Hadoop utilizes `data replication`, `task fragmentation`, and automatic error handling to achieve `fault tolerance` in the face of hardware failures common in large-scale commodity hardware deployments.

• Với việc triển khai trên cụm máy chủ phổ thông 
	• Hỏng hóc phần cứng là chuyện thường ngày, không phải là ngoại lệ 
	• ==Hadoop chịu lỗi thông qua kỹ thuật “dư thừa” ==
• Các tệp tin trong HDFS được phân mảnh, nhân bản ra các nodes trong cụm 
	• Nếu một node gặp lỗi, dữ liệu ứng với nodes đó được tái nhân bản qua các nodes khác 
• Công việc xử lý dữ liệu được phân mảnh thành các tác vụ độc lập 
	• Mỗi tác vụ xử lý một phần dữ liệu đầu vào 
	• Các tác vụ được thực thi song song với các tác vụ khác 
	• Tác vụ lỗi sẽ được tái lập lịch thực thi trên node khác 
==• Hệ thống Hadoop thiết kế sao cho các lỗi xảy ra trong hệ thống được xử lý tự động, không ảnh hưởng tới các ứng dụng phía trên==


# 2.  Understanding HDFS

### 2.1 HDFS Overview: 
>This section introduces the Hadoop Distributed File System (HDFS) as a `cost-effective` and `reliable` storage solution for `large datasets`, optimized for large files with a `hierarchical directory structure` similar to `UNIX`.

• HDFS cung cấp khả năng lưu trữ tin cậy và chi phí hợp lý cho khối lượng dữ liệu lớn 
	• Tối ưu cho các tập tin kích thước lớn (từ vài trăm MB tới vài TB) 
• HDFS có không gian cây thư mục phân cấp như UNIX (vd., `/hust/soict/hello.txt`) 
	• Hỗ trợ cơ chế phân quyền và kiểm soát người dùng như của UNIX 
• Khác biệt so với hệ thống tập tin trên UNIX 
	• Chỉ hỗ trợ thao tác ghi thêm dữ liệu vào cuối tệp (APPEND) 
	• Ghi một lần và đọc nhiều lần
### 2.2 HDFS Architecture: 

![[Pasted image 20241006182734.png|460]]

Architecture của HDFS là Master/Slave architecture
- ==Name node (Master):== quản lý không gian tên và siêu dữ liệu (metadata) mà ánh xạ tới vị trí các chunks ( các khối dữ liệu). Name node sẽ giám sát các data node trong cụm
- ==Data node (Slave):== Data nodes are the worker nodes in an HDFS cluster. Storing actual data chunks and performing I/O operations (reading and writing data) on those chunks. Because HDFS is designed for data redundancy, each chunk is typically replicated across multiple data nodes

### 2.3 Core Design Principles of HDFS: 
#### Append-only Data
	Chỉ ghi thêm (Append)→ giảm chi phí điều khiển tương tranh

HDFS is primarily designed for `write-once, read-many` workloads. This means that once data is written to a file, it is generally considered `immutable` and is not typically updated in place. Instead, new data is appended to the end of the file. This design choice simplifies `data consistency` and `concurrency control`, as it reduces the complexity of managing concurrent writes.
#### Large Data Blocks
• Tệp được chia thành các chunks lớn (64 MB) 
→Giảm kích thước metadata 
→Giảm chi phí truyền dữ liệu (frequency of data transfer)
#### Data replication
- Mỗi chunk thông thường được sao làm 3 nhân bản
#### Fault Tolerance Mechanisms
• Data node: sử dụng cơ chế tái nhân bản 
`If a data node fails, the name node detects the failure and automatically initiates the replication of the lost blocks to other available data nodes.`
• Name node 
	• Sử dụng Secondary Name Node 
	• SNN hỏi data nodes khi khởi động thay vì phải thực hiện cơ chế đồng bộ phức tạp với primary NN
The name node is a single point of failure in HDFS. To mitigate this, HDFS utilizes a secondary name node. While it doesn't actively serve client requests, it periodically communicates with the primary name node to obtain its current state information. In case of a primary name node failure, the secondary name node's information can be used to help recover the file system metadata. However, it's important to note that the secondary name node doesn't provide full redundancy for the name node
# 3. The MapReduce Data Processing Model
> talk about the way we process data in Hadoop ecosystem
### 3.1 Introduction to MapReduce: 

- The default data processing model in Hadoop
- Simplicity, Flexibility, and Scalability. 
- MapReduce is a programming model, not a programming language, and was proposed by Google.
#### 3.2 A MapReduce Job: 

A MapReduce program consists of a sequence of isolated tasks that operate on data.2 These tasks are distributed across the Hadoop cluster for parallel execution, enhancing scalability by minimizing inter-node communication and avoiding complex synchronization mechanisms.2 Data for MapReduce jobs is typically stored in HDFS, and during execution, the MapReduce code is sent to the nodes where the data resides

A MapReduce program is comprised of two fundamental functions: Map and Reduce.3 These functions are executed by processes called "Mappers" and "Reducers," respectively. Data in MapReduce is represented as key-value pairs.3 Both the input and output of the Map and Reduce functions are in this key-value pair format.
#### 3.3 MapReduce Data Handling: 
This section explains that MapReduce in Hadoop typically works with data already present in HDFS, and code is sent to nodes holding relevant data for processing.
- **3.4 Writing MapReduce Programs**: This section explains the structure of a MapReduce program, requiring the implementation of Map and Reduce functions executed by corresponding Mappers and Reducers. It emphasizes that data is viewed as key-value pairs throughout the process.
- **3.5 Illustrative Example**: This section provides a concrete example of a MapReduce job to calculate total sales by employee from a text file containing order ID, employee name, and sale amount information.
- **3.6 Map Phase**: 
In the Map phase, multiple Mapper tasks process the input data independently.5 Each Mapper works on a specific chunk of the input data, usually a block stored in HDFS.5
For each input key-value pair, the Mapper can produce zero or more intermediate key-value pairs.5 In the example provided, a Mapper processes each line of text, emitting the employee name as the key and the corresponding sales amount as the value.
- **3.7 Shuffle & Sort Phase**: Hadoop automatically sorts and groups the intermediate key-value pairs generated by the Mappers into partitions based on the keys.6 These partitions are then fed as input to the Reducers.

Reduce Phase

Reducers receive sorted data from the Shuffle and Sort phase.6 Each Reducer processes all the values associated with a particular key. Similar to the Map phase, the Reducer processes one key at a time, iterating through all its corresponding values.6

Using the example from the source, the Reduce function calculates the total sales for each employee.6 The final output is a set of key-value pairs, where the key is the employee name and the value is the total sales amount
- **3.8 Reduce Phase**: This section details the Reduce phase, where Reducers process sorted data from the Shuffle & Sort phase, receiving all values associated with a particular key, and generating final output key-value pairs.
- **3.9 Data Flow**: This section provides a visual representation of the data flow through the Map, Shuffle & Sort, and Reduce phases in a MapReduce job.
- **3.10 Word Count Example**: This section walks through a specific example of a Word Count program to illustrate the MapReduce data flow and processing steps.
- **3.11 Implementing Word Count**: This section shows a practical implementation of the Word Count program in code.
- **3.12 Distributed MapReduce**: This section explains how MapReduce operates in a distributed environment, highlighting the roles of Job Tracker and Task Tracker in managing and executing tasks across the cluster.

**4. Expanding the Hadoop Ecosystem**

- **4.1 Beyond HDFS and MapReduce**: This section introduces other systems and components within the Hadoop ecosystem that extend its capabilities beyond core storage and processing to include data analysis, integration, workflow management, and more.
- **4.2 Apache Pig**: This section describes Apache Pig, a high-level data processing language and execution framework that simplifies complex data transformations and joins. It explains how Pig scripts are translated into MapReduce jobs for execution on the Hadoop cluster.
- **4.3 Apache Hive**: This section introduces Apache Hive, another high-level abstraction layer over MapReduce that provides a SQL-like language called HiveQL for data querying and analysis. It explains how Hive scripts are compiled into MapReduce jobs for execution on the cluster.
- **4.4 Apache HBase**: This section describes Apache HBase, a distributed, scalable, column-oriented NoSQL database built on top of HDFS. It highlights HBase's capabilities in storing and managing massive datasets with high write throughput and its limitations compared to traditional relational databases.
- **4.5 Apache Sqoop**: This section explains Apache Sqoop, a tool designed for bulk data transfer between Apache Hadoop and structured data stores like relational databases. It outlines Sqoop's capabilities in importing and exporting data using Map-only or MapReduce jobs.
- **4.6 Apache Kafka**: This section introduces Apache Kafka, a distributed streaming platform that decouples data producers and consumers, ensuring flexibility and reliability in data pipelines.
- **4.7 Apache Oozie**: This section describes Apache Oozie, a workflow scheduling system that manages the execution of various tasks within the Hadoop cluster, including MapReduce jobs, Pig and Hive scripts, Java and Shell programs, and other data manipulation and system interaction tasks.
- **4.8 Apache Zookeeper**: This section introduces Apache ZooKeeper, a distributed coordination service that provides reliable distributed coordination primitives like group membership management, leader election, dynamic configuration management, and system state monitoring. It highlights ZooKeeper's critical role in distributed systems.
- **4.9 PAXOS Algorithm**: This section briefly mentions the PAXOS algorithm, a consensus algorithm used in distributed systems, and provides a link to a YouTube video for further exploration.
- **4.10 YARN: Yet Another Resource Negotiator**: This section introduces YARN as the cluster resource manager in Hadoop 2.0 and beyond, responsible for allocating resources like memory and CPU cores to applications on demand. It explains how YARN allows both MapReduce and non-MapReduce applications to run on the same Hadoop cluster.
- **4.11 YARN Resource Allocation**: This section provides an example illustrating how YARN allocates resources to different applications within the cluster.

**5. The Big Picture**

- **5.1 Hadoop Ecosystem Overview**: This section provides a visual overview of the Hadoop ecosystem, showcasing the interconnections and relationships between various components.
- **5.2 Hortonworks Data Platform Sandbox**: This section mentions the Hortonworks Data Platform Sandbox as a tool for exploring and experimenting with the Hadoop ecosystem.
- **5.3 Platform Demonstration**: This section indicates a demonstration of the platform's capabilities.
- **5.4 Big Data Platforms**: This section mentions other big data management platforms.
- **5.5 Conclusion**: This section offers concluding remarks and acknowledgments.