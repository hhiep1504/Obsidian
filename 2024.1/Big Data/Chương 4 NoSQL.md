# I. Introduction to NoSQL Databases

- **Eras of Databases:**
	- Tổng quan về lịch sử của cơ sở dữ liệu, đối chiếu thời kỳ trước NoSQL của Relational Database Management Systems (RDBMS) nguyên khối (monolithic) với sự xuất hiện của nhiều giải pháp NoSQL khác nhau do nhu cầu riêng biệt của các ứng dụng web hiện đại thúc đẩy.
- **Why NoSQL?**:
	- Phần này đi sâu vào những hạn chế của RDBMS truyền thống trong việc xử lý các yêu cầu về quy mô, tính linh hoạt và phân phối của các ứng dụng web. Phần này nêu bật những ưu điểm của cơ sở dữ liệu NoSQL, bao gồm khả năng mở rộng theo chiều ngang - **horizontal scalability**, phân phối theo địa lý - **geographic distribution**, tính linh hoạt của lược đồ - **schema flexibility** và tính thân thiện với nhà phát triển - d**eveloper friendliness**.
- **SQL vs. NoSQL:** 
	- A comparative analysis of SQL and NoSQL databases across various parameters such as data volume, architecture, data structure, query language, and consistency models.
	 ![[Pasted image 20241031001652.png]]

## **II. NoSQL Use Cases and Popularity**

* **NoSQL Use Cases:** 
	* Khám phá các tình huống cụ thể mà cơ sở dữ liệu NoSQL phát huy hiệu quả, chẳng hạn như quản lý khối lượng dữ liệu lớn, xử lý luồng dữ liệu tốc độ cao, đảm bảo tính khả dụng cao và thích ứng với các lược đồ dữ liệu đang phát triển. Các ví dụ thực tế từ những gã khổng lồ trong ngành như Google, Amazon, Yahoo và Facebook được cung cấp.

* **DB Engine Ranking (2019):** 
	* Presents the popularity ranking of different database engines, showcasing the rise of NoSQL solutions within the database landscape.

## **III. Deep Dive into NoSQL Data Models**

- **Relational Data Model Revisited:** 
	- Xem xét các khái niệm cốt lõi của mô hình dữ liệu quan hệ - relational data model, điểm mạnh của nó (ACID transactions, maturity, security) và các hạn chế của nó (scalability, upfront data modeling) trong bối cảnh các thách thức về dữ liệu hiện đại. 
	- Các ví dụ RDBMS phổ biến được cung cấp: Oracle, MySQL, PostgreSQL, Microsoft SQL Server, IBM DB/2

- **Key/Value Data Model:**
	- Giới thiệu tính đơn giản và khả năng mở rộng của mô hình dữ liệu key/value, nhấn mạnh các hoạt động cốt lõi của nó (GET, PUT, DELETE) và tính phù hợp của nó đối với việc truy cập dữ liệu tốc độ cao. 
	- Super fast and easy to scale because not involve joins
	- Các ví dụ về kho lưu trữ key/value như Berkeley DB, Memcache, DynamoDB, Redis và Riak được thảo luận.

- **Key/Value vs. Table and Relational Model:** 
 
	 ![[Pasted image 20241031005045.png]]

- **Memcached:** 
	- Open-source in-memory key-value caching system được biết đến với tốc độ và tính dễ sử dụng trong các ứng dụng web động.

- **Redis:** 
	- Khám phá Redis, một kho lưu trữ open-source in-memory key-value khác mở rộng chức năng với các cấu trúc dữ liệu, tùy chọn lưu trữ liên tục (persistence options) và các tính năng như transactions và pub/sub.

- **Amazon DynamoDB:** 
	- Tập trung vào DynamoDB, một kho lưu trữ khóa-giá trị được quản lý có khả năng mở rộng cao do Amazon cung cấp, được biết đến với khả năng tích hợp với các dịch vụ AWS khác và hiệu suất nhất quán.

- **Riak:**
	- Một kho lưu trữ khóa-giá trị phân tán tập trung vào tính khả dụng, khả năng chịu lỗi (fault tolerance) và khả năng mở rộng (scalability), đồng thời làm nổi bật kiến ​​trúc và các tính năng "lấy cảm hứng từ Dynamo" của kho lưu trữ này.
	
- **Column Family Store:** 
	- Giới thiệu khái niệm về cơ sở dữ liệu theo cột, làm nổi bật các lược đồ động, khả năng xử lý dữ liệu thưa thớt và việc sử dụng các họ cột và siêu cột để tổ chức dữ liệu..
- **Column Families:** Explains how grouping columns into families enhances data retrieval efficiency and scalability.
- **Column Family vs. Relational Model:** Contrasts the column family model with the relational model, emphasizing the sparse matrix structure, extensibility, and hybrid row/column storage approach.
- **Bigtable:** 
	- Khảo sát Bigtable, một hệ thống lưu trữ phân tán mang tính đột phá được thiết kế cho khả năng mở rộng lớn, khả năng chịu lỗi và hiệu suất cao, nhấn mạnh kiến ​​trúc phân tán và khả năng tự quản lý của nó.
- **Apache HBase:** Introduces Apache HBase, an open-source implementation of Bigtable, built on top of Hadoop, highlighting its suitability for large-scale data processing and analysis.
- **Apache Cassandra:** Discusses Apache Cassandra, a distributed column family database known for its linear scalability, peer-to-peer architecture, and resilience.
- **Graph Data Model:** Explains the graph data model, which represents data as nodes and relationships, emphasizing its suitability for interconnected data and its query approach based on graph traversals.
- **Graph Database Store:** Describes the characteristics of graph databases, their optimized traversal capabilities, and their advantages over relational, key-value, and document stores in specific use cases.
- **Linking Open Data:** Highlights the application of graph databases in managing and querying linked open data.
- **Neo4j:** Presents Neo4j, a popular graph database designed for ease of use, ACID compliance, high availability, and scalability, highlighting its features and API options.
- **Document Store:** Introduces the document store model, which stores data in flexible document formats like JSON or XML, emphasizing its schema-less nature and its ability to index document properties.
- **Relational Data Mapping Challenges:** Discusses the complexities of object-relational mapping (ORM) in traditional web development and the associated performance overhead.
- **Web Service as a Middle Tier:** Explains the use of web services to manage data exchange between web applications and relational databases.
- **Document Mapping Simplicity:** Highlights the simplified data management approach offered by document stores, where data is stored and retrieved in native document format, eliminating the need for complex ORM layers.
- **MongoDB:** Presents MongoDB, a widely used open-source document store based on JSON, known for its master-slave replication, sharding capabilities, and developer-friendly features.
- **MongoDB Architecture:** Delves into the architecture of MongoDB, focusing on replica sets for data safety and high availability, and sharding for horizontal scalability.
- **Apache CouchDB:** Introduces Apache CouchDB, an open-source document store with a RESTful API, ACID support, and features like B-Tree indexing, versioning, and data compaction.

**IV. References:** Provides a list of academic papers and resources for further exploration of NoSQL databases.