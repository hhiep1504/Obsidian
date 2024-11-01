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

## Relational Data Model Revisited: 
- Xem xét các khái niệm cốt lõi của mô hình dữ liệu quan hệ - relational data model, điểm mạnh của nó (ACID transactions, maturity, security) và các hạn chế của nó (scalability, upfront data modeling) trong bối cảnh các thách thức về dữ liệu hiện đại. 
- Các ví dụ RDBMS phổ biến được cung cấp: Oracle, MySQL, PostgreSQL, Microsoft SQL Server, IBM DB/2

## Key/Value Data Model:
- Giới thiệu tính đơn giản và khả năng mở rộng của mô hình dữ liệu key/value, nhấn mạnh các hoạt động cốt lõi của nó (GET, PUT, DELETE) và tính phù hợp của nó đối với việc truy cập dữ liệu tốc độ cao. 
- Super fast and easy to scale because not involve joins
- Các ví dụ về kho lưu trữ key/value như Berkeley DB, Memcache, DynamoDB, Redis và Riak được thảo luận.

## Key/Value vs. Table and Relational Model: 
 
![[Pasted image 20241031005045.png]]

## Memcached:
- Memcached is an open-source, in-memory key-value caching system designed to enhance the speed of dynamic web applications by reducing database load. It effectively utilizes RAM across numerous distributed web servers, achieving typical read times of 30ms.
- Key features of Memcached include:
	● A simple interface for managing distributed RAM caches.
	● Quick deployment and ease of development.
	● APIs available in multiple programming languages.

## Redis: 
- Redis, similar to Memcached, is an open-source, in-memory key-value store. It distinguishes itself by offering optional durability, meaning data can persist beyond RAM.
- Key characteristics of Redis include:
	●High-speed read and write operations for commonly used data structures directly in RAM.
	●Support for storing and manipulating simple data structures like lists, sets, and hashes within its values.
	●Developer-friendly features such as expiration, transactions, pub/sub, and partitioning.

## Amazon DynamoDB: 
- Scalable key-value store 
- Fastest growing product in Amazon's history 
- Focus on throughput on storage and predictable read and write times 
- Strong integration with S3 and Elastic MapReduce

## Riak:
- Open source distributed key-value store with support and commercial versions by Basho 
- A "Dynamo-inspired" database 
- Focus on availability, fault-tolerance, operational simplicity and scalability 
- Support for replication and auto-sharding and rebalancing on failures 
- Support for MapReduce, fulltext search and secondary indexes of value tags 
- Written in ERLANG
	
## Column Family Store: 
- Dynamic schema, column-oriented data model 
- Sparse, distributed persistent multi-dimensional sorted map
- (row, column (family), timestamp) -> cell contents
## Column Families: 
- Group columns into "Column families" 
- Group column families into "Super- Columns" 
- Be able to query all columns with a family or super family 
- Similar data grouped together to improve speed
## Column Family vs. Relational Model: 
- Sparse matrix, preserve table structure 
	- One row could have millions of columns but can be very sparse 
- Hybrid row/column stores 
- Number of columns is extendible 
	- New columns to be inserted without doing an "alter table"
![[Pasted image 20241101172251.png]]
## Bigtable: 
- một hệ thống lưu trữ phân tán mang tính đột phá được thiết kế cho 
	- khả năng mở rộng lớn
	- khả năng chịu lỗi và hiệu suất cao
	- nhấn mạnh kiến ​​trúc phân tán
	- khả năng tự quản lý
## Apache HBase:
Introduces Apache HBase, an open-source implementation of Bigtable, built on top of Hadoop, highlighting its suitability for large-scale data processing and analysis.
## Apache Cassandra:
Discusses Apache Cassandra, a distributed column family database known for its linear scalability, peer-to-peer architecture, and resilience.
	- Apache open source column family database 
	- Supported by DataStax 
	- Peer-to-peer distribution model 
	- Strong reputation for linear scale out (millions of writes/second) 
		- Written in Java and works well with HDFS and MapReduce
## Graph Data Model:
Explains the graph data model, which represents data as nodes and relationships, emphasizing its suitability for interconnected data and its query approach based on graph traversals.
	The graph data model centers around three primary abstractions:
	● Nodes: Representing entities or objects within the data.
	● Relationships: Defining connections or associations between nodes.
	● Properties: Attributes or characteristics assigned to both nodes and relationships.

## Graph Database Store: 

A **graph database** stores data using an explicit graph structure. In this model, each node maintains awareness of its adjacent nodes, enabling efficient traversal and analysis of relationships.

##### Advantages of Graph Databases

- **Optimized for Connections:** Graph databases excel in handling complex interconnected data, making them suitable for scenarios where understanding relationships is crucial. For instance, they are well-suited for social networks, recommendation systems, and fraud detection where connections between entities play a significant role.
- **Traversal Efficiency:** Queries in graph databases essentially involve traversing the graph structure. This inherent design allows for fast and efficient retrieval of connected data.

#### Comparison with Other Data Models

- **Relational Databases:** While relational databases are optimized for data aggregation through operations like joins, graph databases shine when exploring connections between data points.
	- ![[Pasted image 20241101172939.png|550]]
- **Key-Value Stores:** Key-value stores are efficient for simple lookups of data based on keys. Graph databases, however, are better suited for navigating interconnected data and understanding relationships. This distinction aligns with our earlier discussion of Memcached and Redis, which are examples of key-value stores focused on speed and simplicity.
	- ![[Pasted image 20241101173001.png|550]]
- **Document Stores:** Document stores are effective for managing hierarchical or tree-like data structures. Graph databases, on the other hand, go beyond this by capturing the intricate network of relationships, offering a more comprehensive view of the data landscape.
	- ![[Pasted image 20241101173016.png|550]]

## Neo4j

Neo4j is a prominent example of a graph database. According to the sources, it offers the following features:

- Ease of Use: Specifically designed with Java developers in mind.
- Persistence: Data is stored on disk, ensuring permanence beyond RAM.
- ACID Compliance: Guarantees atomicity, consistency, isolation, and durability of transactions.
- High Availability: The Enterprise Edition of Neo4j ensures high availability.
- Scalability: Can handle a vast number of nodes, relationships, and properties.
- Accessibility: Provides both an embedded Java library and a REST API for interaction.


## Document Store: 
Introduces the document store model, which stores data in flexible document formats like JSON or XML, emphasizing its schema-less nature and its ability to index document properties.
	• Documents, not value, not tables 
	• JSON or XML formats 
	• Document is identified by ID 
	• Allow indexing on properties
			![[Pasted image 20241101173959.png]]

Relational data mapping is a technique used to bridge the gap between object-oriented programming in application development and the structured, tabular format of relational databases. The sources provide a specific example of this mapping in the context of web applications, outlining various transformations (T1-T6) involved in this process.
## Transformations in Relational Data Mapping

- **T1 (HTML to Objects):** Web browser input, typically in HTML format, is converted into Java                                       objects within the application's middle tier.
- **T2 (Objects to SQL Tables):** These Java objects are then mapped and stored into relational                                               database tables using SQL (Structured Query Language).
- **T3 (Tables to Objects):** When data is retrieved from the database, it is transformed back                                            into Java objects for processing within the application.
- **T4 (Objects to HTML):** Finally, these objects are converted back into HTML for display in                                           the web browser.
![[Pasted image 20241101174209.png]]

 when a web service is introduced into this architecture:

- **T5 (Objects to XML):** Java objects are serialized into XML (Extensible Markup Language) for                                   communication with the web service.
- **T6 (XML to Objects):** XML data received from the web service is deserialized back into Java                                    objects for further processing within the application.
![[Pasted image 20241101174224.png]]

## Challenges and Alternatives

Object-relational mapping has become increasingly complex in modern application development. Frameworks like Java Hibernate and JPA (Java Persistence API) have emerged to address these complexities.

However, the sources suggest that maintaining a simple architecture can help avoid such challenges. This is where **document mapping** comes into play as an alternative to relational data mapping.

## Document Mapping

Document mapping involves a more direct correspondence between documents in the database and documents in the application, eliminating the need for an object middle tier and the associated complexities of object-relational mapping. This approach simplifies data handling by avoiding the processes of "shredding" data into relational tables and then reassembling it back into objects.

## Document Databases

**MongoDB** and **Apache CouchDB** are examples of document databases that support this approach. They store data in flexible document formats like JSON (JavaScript Object Notation) or XML, allowing for a more natural representation of data structures commonly used in applications.

### MongoDB 
• Open Source JSON data store created by 10gen 
• Master-slave scale out model 
• Strong developer community 
• Sharding built-in, automatic 
• Implemented in C++ with many APIs (C++, JavaScript, Java, Perl, Python etc.)
### Apache CouchDB 
• Apache project 
• Open source JSON data store 
• Written in ERLANG 
• RESTful JSON API 
• B-Tree based indexing, shadowing b-tree versioning 
• ACID fully supported 
• View model 
• Data compaction 
• Security



**IV. References:** Provides a list of academic papers and resources for further exploration of NoSQL databases.