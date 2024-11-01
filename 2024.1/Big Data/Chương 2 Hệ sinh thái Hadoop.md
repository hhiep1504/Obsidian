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

A MapReduce job is a program that is broken down into numerous independent tasks and distributed across different nodes in a cluster for execution. Each task operates independently to enhance scalability. This approach minimizes communication between server nodes and avoids synchronization between tasks. 
![[Pasted image 20241008184226.png|600]]

A MapReduce program consists of two functions: Map and Reduce. These functions are executed by Mapper and Reducer processes. Data in MapReduce is treated as key-value pairs. The Map and Reduce functions take key-value pairs as input and return output in the same format. 
![[Pasted image 20241008184136.png|600]]


MapReduce is the default data processing paradigm in Hadoop. It was proposed by Google and is characterized by its simplicity, flexibility, and scalability.

#### 3.3 Illustrative Example: 

Here is an example of MapReduce:

- **Input:** A text file containing order ID, employee name, and sale amount.
- **Output:** Sales by each employee.

			![[Pasted image 20241008184704.png|300]]

**Map Phase**

- The input data is processed by multiple independent Mapping tasks.
- The number of Mapping tasks is determined by the amount of input data (approximately the number of chunks).
- Each Mapping task processes a portion of the data (chunk) from the original data block.
- For each Mapping task, the Mapper processes each input record sequentially.
- For each input record (key-value), the Mapper outputs zero or more output records (intermediate key-value).
- In this example, the Mapping task simply reads each line of text and outputs the employee name and corresponding sales amount.
		![[Pasted image 20241008185121.png|500]]
**Shuffle & Sort Phase**

- Hadoop automatically sorts and groups the Mappers' output by partitions.
- Each partition is the input for a Reducer.
	![[Pasted image 20241008185216.png|550]]

**Reduce Phase**

- The Reducer receives input data from the shuffle & sort step.
- All key-value records corresponding to a key are processed by a single Reducer.
- Similar to the Map step, the Reducer processes each key sequentially, each time with all the corresponding values.
- In the example, the reduce function simply sums the sales for each employee, the output is key-value pairs corresponding to employee name - total sales.

	![[Pasted image 20241008185314.png|550]]
#### 3.4 Map Phase: 
In the Map phase, multiple Mapper tasks process the input data independently. Each Mapper works on a specific chunk of the input data, usually a block stored in HDFS.
For each input key-value pair, the Mapper can produce zero or more intermediate key-value pairs. In the example provided, a Mapper processes each line of text, emitting the employee name as the key and the corresponding sales amount as the value.
#### 3.5 Shuffle & Sort Phase: 
Hadoop automatically sorts and groups the intermediate key-value pairs generated by the Mappers into partitions based on the keys. These partitions are then fed as input to the Reducers.

#### 3.6 Reduce Phase

Reducers receive sorted data from the Shuffle and Sort phase. Each Reducer processes all the values associated with a particular key. Similar to the Map phase, the Reducer processes one key at a time, iterating through all its corresponding values.6

Using the example from the source, the Reduce function calculates the total sales for each employee. The final output is a set of key-value pairs, where the key is the employee name and the value is the total sales amount

#### 3.7 Data Flow: 

![[Pasted image 20241008185424.png]]
#### 3.10 Word Count Example: 
This section walks through a specific example of a Word Count program to illustrate the MapReduce data flow and processing steps.
![[Pasted image 20241008190732.png]]
#### 3.11 Implementing Word Count: 
This section shows a practical implementation of the Word Count program in code.
#### 3.12 Distributed MapReduce: 

>MapReduce processes data in a distributed environment by breaking down large datasets into smaller chunks and distributing them across multiple nodes in a cluster. Here's how it works:

	![[Pasted image 20241008191101.png|600]]

- **Data Locality:** MapReduce prioritizes processing data where it's stored to reduce data transfer overhead. The input data, typically stored in HDFS, is divided into chunks, and Map tasks are assigned to nodes containing those chunks.
- **Parallel Processing:** Multiple Mapper tasks can run concurrently on different nodes, each processing a separate chunk of the data. This parallel execution significantly speeds up the processing of large datasets.
- **Shuffle and Sort:** After the Map phase, Hadoop shuffles and sorts the intermediate key-value pairs produced by the Mappers. This ensures that all values associated with a specific key are sent to the same Reducer.
- **Reducer Tasks:** Reducers process the sorted data received from the Mappers, aggregating and summarizing the results. Like Mappers, Reducers can also run in parallel on different nodes, improving efficiency.
- **Fault Tolerance:** In a distributed environment, node failures are common. Hadoop's MapReduce is designed to handle such failures. If a node running a task fails, the task is automatically restarted on a different node.

**JobTracker and TaskTracker (Hadoop 1.0)**:

		![[Pasted image 20241008191211.png|450]]

- In earlier Hadoop versions (1.0), JobTracker and TaskTracker were key components for managing distributed execution:
    - **JobTracker:** Responsible for dividing jobs into tasks, scheduling those tasks across the cluster, and monitoring their progress.
    - **TaskTracker:** Ran on each node in the cluster, communicating with the JobTracker to receive tasks and report their status.


# 4. Expanding the Hadoop Ecosystem

#### 4.1 Beyond HDFS and MapReduce: 
Ngoài HDFS và MapReduce, hệ sinh thái Hadoop còn nhiều hệ thống, thành phần khác phục vụ 
	• Phân tích dữ liệu 
	• Tích hợp dữ liệu 
	• Quản lý luồng 
	• Vvv 
Các thành phần này không phải là ‘core Hadoop’ nhưng là 1 phần của hệ sinh thái Hadoop 
	• Hầu hết là mã nguồn mở trên Apache
#### 4.2 Apache Pig: 
- A high-level data processing language and execution framework
- Pig đặc biệt tốt cho các phép toán Join và Transformation. 
Execution Flow:
- The Pig compiler, which runs on a client machine, translates Pig Latin scripts into a series of MapReduce jobs.
- These MapReduce jobs are then submitted to the Hadoop cluster for execution
#### 4.3 Apache Hive: 
Another high-level abstraction layer over MapReduce that provides a SQL-like language called HiveQL for data querying and analysis.

Hive thường được sử dụng để tạo hệ thống kho dữ liệu trên Hadoop. Nó cung cấp các công cụ và tính năng để sắp xếp dữ liệu thành các bảng và phân vùng, xác định lược đồ và áp dụng các kiểu dữ liệu, tương tự như kho dữ liệu truyền thống.

**Thực thi thông qua MapReduce:**
* Khi người dùng gửi truy vấn HiveQL, trình biên dịch Hive (chạy trên máy khách) sẽ dịch truy vấn đó thành một loạt các tác vụ MapReduce. Các tác vụ này được tối ưu hóa để thực thi trong cụm Hadoop.
* Các tác vụ MapReduce đã dịch sau đó được gửi đến cụm Hadoop để thực thi, tận dụng khả năng xử lý phân tán của Hadoop để xử lý các tập dữ liệu lớn.

#### 4.4 Apache HBase: 
- HBase là một CSDL cột mở rộng phân tán, lưu trữ dữ liệu trên HDFS 
	• Được xem như là hệ quản trị CSDL của Hadoop 
• Dữ liệu được tổ chức về mặt logic là các bảng, bao gồm rất nhiều dòng và cột 
	• Kích thước bảng có thể lên đến hàng Terabyte, Petabyte 
	• Bảng có thể có hàng ngàn cột 
• Có tính khả mở cao, đáp ứng băng thông ghi dữ liệu tốc độ cao 
	• Hỗ trợ hàng trăm ngàn thao tác INSERT mỗi giây (/s) 
• Tuy nhiên về các chức năng thì còn rất hạn chế khi so sánh với hệ QTCSDL truyền thống 
	• Là NoSQL : không có ngôn ngữ truy vấn mức cao như SQL 
	• Phải sự dụng API để scan/ put/ get/ dữ liệu theo khóa.
#### 4.5 Apache Sqoop: 
• Sqoop là một công cụ cho phép trung chuyển dữ liệu theo khối từ Apache Hadoop và các CSDL có cấu trúc như CSDL quan hệ 
• Hỗ trợ import tất cả các bảng, một bảng hay 1 phần của bảng vào HDFS 
	• Thông qua Map only hoặc MapReduce job 
	• Kết quả là 1 thư mục trong HDFS chứ các tập tin văn bản phân tách các trường theo ký tự phân tách (vd. , hoặc \t) 
• Hỗ trợ export dữ liệu ngược trở lại từ Hadoop ra bên ngoài

			![[Pasted image 20241008193250.png|400]]
### 4.6 Apache Kafka: 
![[Pasted image 20241008193324.png]]
#### 4.7 Apache Oozie: 
• Oozie là một hệ thống lập lịch luồng công việc để quản lý các công việc thực thi trên cụm Hadoop 
• Luồng workflow của Oozie là đồ thị vòng có hướng (Directed Acyclical Graphs (DAGs)) của các khối công việc 
• Oozie hỗ trợ đa dạng các loại công việc 
	• Thực thi MapReduce jobs 
	• Thực thi Pig hay Hive scripts 
	• Thực thi các chương trình Java hoặc Shell 
	• Tương tác với dữ liệu trên HDFS 
	• Chạy chương trình từ xa qua SSH 
	• Gửi nhận email
#### 4.8 Apache Zookeeper: 
This section introduces Apache ZooKeeper, a distributed coordination service that provides reliable distributed coordination primitives like group membership management, leader election, dynamic configuration management, and system state monitoring. It highlights ZooKeeper's critical role in distributed systems.

• Apache ZooKeeper là một dịch vụ cung cấp các chức năng phối hợp phân tán độ tin cậy cao 
	• Quản lý thành viên trong nhóm máy chủ 
	• Bầu cử leader 
	• Quản lý thông tin cấu hình động 
	• Giám sát trạng thái hệ thống 
• Đây là các service lõi, tối quan trọng trong các hệ thống phân tán
#### 4.9 PAXOS Algorithm: 
This section briefly mentions the PAXOS algorithm, a consensus algorithm used in distributed systems, and provides a link to a YouTube video for further exploration.
#### 4.10 YARN: 
• Nodes có tài nguyên là – bộ nhớ và CPU cores 
• YARN đóng vai trò cấp phát lượng tài nguyên phù hợp cho các ứng dụng khi có yêu cầu 
• YARN được đưa ra từ Hadoop 2.0 
	• Cho phép MapReduce và non MapReduce cùng chạy trên 1 cụm Hadoop 
	• Với MapReduce job, vai trò của job tracker được thực hiện bởi application tracker
		![[Pasted image 20241008193622.png|500]]
# 5. The Big Picture

![[Pasted image 20241008193508.png]]

- **5.1 Hadoop Ecosystem Overview**: This section provides a visual overview of the Hadoop ecosystem, showcasing the interconnections and relationships between various components.
- **5.2 Hortonworks Data Platform Sandbox**: This section mentions the Hortonworks Data Platform Sandbox as a tool for exploring and experimenting with the Hadoop ecosystem.
- **5.3 Platform Demonstration**: This section indicates a demonstration of the platform's capabilities.
- **5.4 Big Data Platforms**: This section mentions other big data management platforms.
- **5.5 Conclusion**: This section offers concluding remarks and acknowledgments.