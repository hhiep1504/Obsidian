 # I. Introduction to File Systems

### A. File Systems: Concepts and Definitions:
>This section defines basic file system terminology, including filenames, directories, metadata, and fundamental file operations (READ, WRITE, CREATE, DELETE).

• Filenames 
	• File Identity 
• Directories (folders) 
	• Group of files in separate collections 
• Metadata 
	• Creation time, last access time, last modification time 
	• Security information (Owner, Group owner) 
	• Mapping file to its physical location of file (e.g. location in storage devices) 
• Computer file 
	• A resource for storing information 
	• Durable, remained available for access 
	• Data: sequences of bits 
• File system 
	• Control how computer file are stored and retrieved 
	• Main operators: READ, WRITE (offset, size), CREATE, DELETE
### B. Local vs. Distributed File Systems:
>The section distinguishes between file systems residing on a single machine (local) and those spanning multiple machines (distributed), laying the groundwork for understanding the complexities of distributed systems.

**II. Delving into Distributed File Systems**

- **A. Defining Distributed File Systems:** A detailed explanation of distributed file systems and their role in abstracting storage across multiple devices to provide a unified view for remote processes.
- **B. Benefits of Distributed File Systems:** This section highlights the key advantages of using distributed file systems, including enhanced file sharing, consistent system views for clients, and centralized administration.

**III. Key Goals and Design Principles**

- **A. Achieving Network Transparency:** Discusses the importance of network transparency in distributed file systems, ensuring users can access files seamlessly regardless of location. It delves into concepts like location transparency and location independence.
- **B. Ensuring High Availability:** Explores the crucial role of availability in distributed file systems. It explains how replication techniques help guarantee quick and easy access to files despite potential system failures or heavy user loads.

**IV. Exploring Distributed File System Architectures**

- **A. Client-Server Architecture:** Provides an in-depth look at the client-server model, a popular architecture for distributed file systems like NFS and GFS. It explains how file servers manage storage and handle client requests.
- **B. Symmetric (Peer-to-Peer) Architecture:** Introduces the symmetric architecture based on peer-to-peer technology, highlighting its decentralized nature. Examples like the Ivy system using Chord DHT are provided.

**V. Critical Design Issues in Distributed File Systems**

- **A. Naming and Name Resolution:** This section addresses the complexities of naming and name resolution in distributed environments. It covers concepts like namespaces and traditional name resolution methods.
- **B. File Sharing Semantics and Consistency:** Discusses the challenges of managing concurrent file access in distributed systems. Different file sharing semantic models like UNIX, session, and immutable-shared-files are explored, along with the concept of transactions for ensuring data consistency.
- **C. Caching Strategies and Trade-offs:** Explores various caching mechanisms used in distributed file systems, including server-side and client-side caching (both in memory and on disk). It analyzes the benefits of caching for performance and the trade-offs involved, particularly the cache consistency problem.
- **D. Replication for Reliability and Availability:** This section focuses on replication as a core strategy for enhancing reliability and availability in distributed file systems. It explains the goals of replication and addresses challenges related to maintaining consistency across replicas in the face of server failures or network partitions.