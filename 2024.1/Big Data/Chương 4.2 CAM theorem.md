## I. Scaling Traditional Databases (RDBMS)

**vertical scaling** (upgrading hardware) and **horizontal scaling** (adding more machines) **database sharding** (dividing data across multiple machines) and **replication** (copying data across servers)

**A. Vertical Scaling (Up)**

- This involves upgrading hardware (*e.g., faster CPU, more memory, or larger disk*) for better performance but is limited by the capacity of a single machine *(the amount of CPU, RAM and disk)*.

**B. Horizontal Scaling (Out)**

- Adding more machines through database sharding and replication.
- Faces challenges with complex queries, Read-to-Write ratio, and communication overhead.

**C. Data Sharding**

- Data is divided across servers for parallel access, but complex query processing becomes difficult.

**D. Data Replication**

- Data is copied across servers to avoid bottlenecks and single points of failure, enhancing scalability and availability.
- Creates the challenge of maintaining consistency between replicated data.
	- example: 
		- a bank database is replicated across two servers. 
		- If an event adds $1000 to the balance on one server and another event adds 5% interest on the other server, maintaining consistency becomes difficult.

### II. The Two-Phase Commit Protocol (2PC)

**A. Phase I: Voting**

- The coordinator requests a vote from participant servers to commit the transaction.
![[Pasted image 20241101180610.png]]

**B. Phase II: Commit**

- If all participants vote to commit, the coordinator instructs them to commit locally.
- Ensures atomicity and consistency but can be complex and impact performance.
	![[Pasted image 20241101180622.png]]
### III. The CAP Theorem

**A. Core Concepts**

- Explains the trade-offs in distributed databases between Consistency, Availability, and Partition Tolerance.
	- Consistency: every node always sees the same data at any given instance (i.e., strict consistency) 
	- Availability: the system continues to operate, even if nodes in a cluster crash, or some hardware or software parts are down due to upgrades 
	- Partition Tolerance: the system continues to operate in the presence of network partitions

***CAP theorem:*** 
>any distributed database with shared data, can have at most **two of the three** desirable properties, C, A or P. These are trade-offs involved in distributed system by Eric Brewer in PODC 2000.

![[Pasted image 20241101180852.png]]

**B. Proof of Concept**

- Illustrates using a two-node scenario how achieving all three properties is impossible in a distributed system.

**C. Implications for Relational Databases**

- Traditional relational databases, built on the principle of ACID (Atomicity, Consistency, Isolation, Durability), strive for all three properties, making them difficult to scale horizontally.6

### IV. Large-Scale Databases and Consistency Trade-offs

**A. Availability Prioritization**

- Companies like Google and Amazon prioritize availability to avoid revenue loss from downtime.
- Horizontal scaling increases the risk of failures, demanding a trade-off on strict consistency.

**B. Balancing Consistency and Scalability**

- Applications determine the level of "good-enough" consistency required.
- Strict consistency is difficult to implement and inefficient, while loose consistency offers easier implementation and better efficiency.
	- ![[Pasted image 20241101181140.png]]
### V. The BASE Properties

**A. Embracing Relaxed ACID Guarantees**

- The CAP theorem leads to databases that prioritize availability and partition tolerance over strict consistency.
- The BASE properties (Basically Available, Soft-State, Eventual Consistency) define these relaxed guarantees.
	• Basically Available: the system guarantees Availability 
	• Soft-State: the state of the system may change over time 
	• Eventual Consistency: the system will eventually become consistent

**B. Eventual Consistency**

- Replicas gradually achieve consistency when updates stop, but inconsistencies can occur during updates.
- Read-after-write consistency (e.g., Amazon S3) ensures that clients see their own updates, while protocols like Read Your Own Writes (RYOW) address inconsistencies across replicas.