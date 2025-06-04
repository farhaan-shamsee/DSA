# System Design

## Scalability

Scalability is the ability of a system to handle increased load or traffic by adding resources without significant changes to the architecture. It is crucial for applications that expect growth in users, data, or features.

### Key Concepts

1. **Growth Factors**:
    - **More Users**: As the user base grows, the system must handle more requests.
      - Example: A social media platform experiencing a surge in new users.
    - **Features**: Adding new features can increase complexity and resource requirements.
      - Example: An e-commerce website adding support for a new payment method.
    - **Data**: More data means more storage and processing needs.
      - Example: A video streaming platform like youtube storing more video content over time.
    - **Complexity**: Increased features and data can lead to more complex interactions and dependencies.
      - Example: A system that started as a simple application is broken into smaller, independent systems.
    - **Geographies**: Serving users in different regions can introduce latency and require distributed systems.
      - Example: An e-commerce company launching websites and distribution in new international markets.
2. **Types of Scalability**:
    - **Vertical Scaling (Scale Up)**: Adding more power (CPU, RAM) to an existing server. This is often limited by hardware constraints.
      - Example: Upgrading a server from 16GB to 64GB of RAM to handle more requests.
    - **Horizontal Scaling (Scale Out)**: Adding more servers to distribute the load. This is more flexible and can handle larger traffic.
      - Example: A web application using multiple servers behind a load balancer to handle increased traffic.
    - **Load Balancing**: Distributing incoming traffic across multiple servers to ensure no single server is overwhelmed.
      - Example: Google employs load balancing extensively across its global infrastructure to distribute search queries and traffic evenly across its massive server farms.
    - **Caching**: Storing frequently accessed data in-memory to reduce load on the database or server.
      - Example: Reddit uses caching to store frequently accessed content like hot posts and comments so that they can be served quickly without querying the database each time.
    - **Content Delivery Networks (CDNs)**: Distributing static assets (images, videos, etc.) closer to users to reduce latency and improve load times.
    - **Sharding/Partitioning**: Splitting data or functionality across multiple nodes/servers to distribute workload and avoid bottlenecks.
      - Example: Amazon DynamoDB uses partitioning to distribute data and traffic for its NoSQL database service across many servers, ensuring fast performance and scalability.
      - ![image](https://github.com/user-attachments/assets/b26566a9-ea12-49ac-902b-be9a92e68f30)

    - **Asynchronous Communication**: Deferring long-running or non-critical tasks to background queues or message brokers to keep the main application responsive.
      - Example: Slack uses asynchronous communication for messaging. When a message is sent, the sender's interface doesn't freeze; it continues to be responsive while the message is processed and delivered in the background.
    - **Microservices Architecture**: Breaking down an application into smaller, independent services that can be scaled independently.
      - Example: Uber has evolved its architecture into microservices to handle different functions like billing, notifications, and ride matching independently, allowing for efficient scaling and rapid development.
    - **Auto-Scaling**: Automatically adjusting the number of active servers based on current load to handle spikes in traffic without manual intervention.
    - **Multi-region Deployment**: Deploying the application in multiple data centers or cloud regions to reduce latency and improve redundancy.
      - Example: Spotify uses multi-region deployments to ensure their music streaming service remains highly available and responsive to users all over the world, regardless of where they are located.


## Availability

Availability refers to the system's ability to remain operational and accessible to users, even in the face of failures or high traffic. High availability is crucial for applications that require constant uptime.

It is usually expressed as a percentage, indicating the system's uptime over a specific period.

The formal definition of availability is: **Availability = Uptime / (Uptime + Downtime)**

- **Uptime**: The period during which a system is functional and accessible.
- **Downtime**: The period during which a system is unavailable due to failures, maintenance, or other issues.

### Availability Tiers

![image](https://github.com/user-attachments/assets/69359ff2-32b5-4862-ae17-ba4f6133d3f0)

### Strategies for Improving Availability

1. **Redundancy**: Implementing redundant components (servers, databases) to ensure that if one fails, others can take over.
   - **Example**: A web application using multiple web servers behind a load balancer to ensure that if one server goes down, others can still serve requests.
   - **Techniques**:
     - Server Redundancy: Deploying multiple servers to handle requests, ensuring that if one server fails, others can continue to provide service.
     - Database Redundancy: Creating a replica database that can take over if the primary database fails.
     - Geographic Redundancy: Distributing resources across multiple geographic locations to mitigate the impact of regional failures.

1. **Load Balancing**: Distributing incoming traffic across multiple servers to ensure no single server is overwhelmed.
   - **Example**: A cloud-based application using a load balancer to distribute requests evenly across multiple instances, ensuring high availability even during traffic spikes.
   - **Techniques**:
     - Hardware Load Balancers: Dedicated devices that distribute traffic across multiple servers.
     - Software Load Balancers: Applications that perform load balancing, such as Nginx or HAProxy.

1. **Failover Mechanisms**: Automatically switching to a backup system or component in case of failure.
   - **Example**: A database system that automatically switches to a replica if the primary database fails.
   - **Techniques**:
     - Active-Passive Failover: One server is active while another is on standby, ready to take over in case of failure.
     - Active-Active Failover: Multiple servers are active and can handle requests simultaneously, providing redundancy and load balancing.
1. **Data Replication**: Keeping copies of data across multiple locations to ensure that data is not lost and can be accessed even if one location fails.
   - **Example**: A cloud storage service replicating user data across multiple data centers to ensure availability in case of a regional outage.
   - **Techniques**:
     - Synchronous Replication: Data is written to multiple locations simultaneously, ensuring consistency but potentially increasing latency.
     - Asynchronous Replication: Data is written to one location first and then replicated to others, reducing latency but risking temporary inconsistency.
1. **Monitoring and Alerting**: Continuously monitoring system health and performance to detect issues early and alert the relevant teams.
   - **Example**: A monitoring system that tracks server health and sends alerts if a server goes down or performance degrades.
   - **Techniques**:
     - Health Checks: Regularly checking the status of servers and services to ensure they are operational.
     - Alerting Systems: Using tools like PagerDuty or Slack to notify teams of issues in real-time.
     - Heartbeat Monitoring: Implementing heartbeat signals to check the status of critical components and services.

### Best Practices for High Availability

1. **Design for Failure**: Assume that components will fail and design the system to handle failures gracefully.
   - Example: Implementing retry logic for failed requests and fallback mechanisms for critical services.
2. **Implement Health Checks**: Regularly check the health of components and services to detect issues early.
   - Example: Using tools like Prometheus or Grafana to monitor system health and performance metrics.
3. Use Multiple Availability Zones: Distribute your system across different data centers to prevent localized failures.
4. Practice Chaos Engineering: Intentionally introduce failures to test system resilience.
5. Implement Circuit Breakers: Prevent cascading failures by quickly cutting off problematic services.
6. Use Caching Wisely: Caching can improve availability by reducing load on backend systems.
7. Plan for Capacity: Ensure your system can handle both expected and unexpected load increases.

## CAP Theorem

The CAP theorem states that a distributed data store can only provide two of the following three guarantees at the same time:

1. **Consistency**: Every read receives the most recent write or an error.
2. **Availability**: Every request receives a response, without guarantee that it contains the most recent write.
3. **Partition Tolerance**: The system continues to operate despite network partitions.

**It is impossible for a distributed data store to simultaneously provide all three guarantees.**

## 3 Pillars of CAP

### Consistency

Consistency ensures that every read receives the most recent write or an error. This means that all working nodes in a distributed system will return the same data at any given time.

In a consistent distributed system, if you write data to node A, a read operation from node B will immediately reflect the write operation on node A.

Consistency is crucial for applications where having the most up-to-date data is critical, such as financial systems, where a balance inquiry must reflect the most up-to-date state of an account.

### Availability

Availability guarantees that every request (read or write) receives a response, without ensuring that it contains the most recent write. This means that the system remains operational and responsive, even if the response from some of the nodes don’t reflect most up-to-date data.

Availability is important for applications that need to remain operational at all times, such as online retail systems.

### Partition Tolerance

Partition Tolerance means that the system continues to function despite network partitions where nodes cannot communicate with each other.

When there is a network partition, the system must choose between Consistency and Availability.

## The CAP Trade-Off: Choosing 2 out of 3

The CAP theorem asserts that in the presence of a network partition, a distributed system must choose between Consistency and Availability.

### CP (Consistency and Partition Tolerance):

- These systems prioritize consistency and can tolerate network partitions, but at the cost of availability. During a partition, the system may reject some requests to maintain consistency.

- Traditional relational databases, such as MySQL and PostgreSQL, when configured for strong consistency, prioritize consistency over availability during network partitions.

- Banking systems typically prioritize consistency over availability since data accuracy is more critical than availability during network issues.

- Consider an ATM network for a bank. When you withdraw money, the system must ensure that your balance is updated accurately across all nodes (consistency) to prevent overdrafts or other errors.

### AP (Availability and Partition Tolerance):

- These systems ensure availability and can tolerate network partitions, but at the cost of consistency. During a partition, different nodes may return different values for the same data.

- NoSQL databases like Cassandra and DynamoDB are designed to be highly available and partition-tolerant, potentially at the cost of strong consistency.

- Amazon's shopping cart system is designed to always accept items, prioritizing availability. When you add items to your Amazon cart, the action almost never fails, even during high traffic periods like Black Friday.

### CA (Consistency and Availability):

- In the absence of partitions, a system can be both consistent and available. However, network partitions are inevitable in distributed systems, making this combination impractical.

- Example Systems: Single-node databases can provide both consistency and availability but aren't partition-tolerant. In a distributed setting, this combination is theoretically impossible.

## ACID Transactions

ACID is an acronym that refers to the set of 4 key properties that define a transaction: Atomicity, Consistency, Isolation, and Durability.

### 1. Atomicity

Atomicity ensures that a transaction—comprising multiple operations—executes as a single and indivisible unit of work: it either fully succeeds (commits) or fully fails (rolls back).

If any part of the transaction fails, the entire transaction is rolled back, and the database is restored to a state exactly as it was before the transaction began.

Example: In a money transfer transaction, if the credit step fails, the debit step cannot be allowed to stand on its own. This prevents inconsistent states like “money disappearing” from one account without showing up in another.

#### How Databases Implement Atomicity:

1. Transaction Logs (Write-Ahead Logs):
   1. Every operation is recorded in a write-ahead log before it’s applied to the actual database table.
   2. If a failure occurs, the database uses this log to undo incomplete changes.
2. Commit/Rollback Protocols:
   1. Databases provide commands like BEGIN TRANSACTION, COMMIT, and ROLLBACK
   2. Any changes made between BEGIN TRANSACTION and COMMIT are considered “in-progress” and won’t be permanently applied unless the transaction commits successfully.
   3. If any step fails, or if you explicitly issue a ROLLBACK, all changes since the start of the transaction are undone.

### 2. Consistency

Consistency in the context of ACID transactions ensures that any transaction will bring the database from one valid state to another valid state—never leaving it in a broken or “invalid” state.

It means that all the data integrity constraints, such as primary key constraints (no duplicate IDs), foreign key constraints (related records must exist in parent tables), and check constraints (age can’t be negative), are satisfied before and after the transaction.

If a transaction tries to violate these rules, it will not be committed, and the database will revert to its previous state.

#### How Databases Implement Consistency:

1. Database Schema Constraints:
   1. NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK
2. Triggers and Stored Procedures: Triggers can automatically check additional rules whenever rows are inserted, updated, or deleted.
3. Application-Level Safeguards: While the database enforces constraints at a lower level, applications often add extra checks—like ensuring business rules are followed or data is validated before it even reaches the database layer.

### 3. Isolation

Isolation ensures that concurrently running transactions do not interfere with each other’s intermediate states.

Essentially, while a transaction is in progress, its updates (or intermediate data) remain invisible to other ongoing transactions—giving the illusion that each transaction is running sequentially, one at a time.

This prevents issues like dirty reads (reading uncommitted data), non-repeatable reads (data changes between reads), and phantom reads (new rows appearing in subsequent reads).

#### How Databases Implement Isolation:

1. Locking Mechanisms:
   1. Row-Level Locks: Only the rows being modified are locked, allowing other transactions to read unaffected rows.
   2. Table-Level Locks: Locks the entire table, preventing any other transaction from reading or writing until the lock is released.
   3. Can lead to blocking or deadlocks if multiple transactions compete for the same locks.
2. Multi-Version Concurrency Control (MVCC):
   1. Optimistic Concurrency Control: Instead of blocking reads, the database keeps multiple versions of a row. Readers see a consistent snapshot of data (like a point-in-time view), while writers create a new version of the row when updating.
3. Snapshot Isolation: A form of MVCC where each transaction sees data as it was at the start (or a consistent point) of the transaction.

### 4. Durability

Durability ensures that once a transaction has been committed, the changes it made will survive, even in the face of power failures, crashes, or other catastrophic events.

In other words, once a transaction says “done,” the data is permanently recorded and cannot simply disappear.

#### How Databases Implement Durability:

1. Transaction Logs (Write-Ahead Logging)
2. Replication / Redundancy
3. Backups


## 15 Types of Databases and When to Use Them

1. **Relational Databases (RDBMS)**: 
   1. Relational databases structure data into one or more tables of rows and columns, with a unique key identifying each row. Rows in a table can be linked to rows in other tables through foreign keys, establishing a relationship between them.
   2. Examples: MySQL, PostgreSQL, Oracle, Microsoft SQL Server.
2. **Key-Value Stores**:
   1. Key-value stores are NoSQL databases that store data as key-value pairs providing fast retrieval of values based on unique keys.
   2. They are primarily used when the data model is based on key-value pairs and requires high scalability, availability and throughput.
   3. However, they may not be the best fit for applications that require complex querying, data relationships, or strong consistency guarantees.
   4. Examples: Redis, Amazon DynamoDB.
   5. Common use cases:
      1. Session Storage: Storing and managing user session information such as user preferences, shopping carts or authentication tokens in web applications.
      2. Caching: Implementing caching mechanisms to improve the performance of web applications by storing frequently accessed data in memory for rapid retrieval.
      3. Real-time data processing: Key-value stores can quickly store and retrieve data for real-time analytics, event processing, or message queues.
3. **Document Stores**:
   1. Document databases, a subset of the broader NoSQL family, are designed to store, manage, and retrieve document-oriented information.
   2. These databases handle data in a semi-structured format, typically JSON, XML, or BSON, allowing for a more flexible schema than traditional relational databases.
   3. Examples: MongoDB, CouchDB, Amazon DocumentDB.
   4. Common use cases:
      1. Content Management Systems (CMS): Storing and managing content such as articles, blog posts, and user-generated content in a flexible schema.
      2. E-commerce Applications: Managing product catalogs, user profiles, and order histories with varying attributes.
      3. Real-time Analytics: Storing and analyzing large volumes of semi-structured data for real-time insights.
4. **Graph Databases**:
   1. Graph databases are a type of NoSQL database that specialize in storing, managing, and querying complex networks of interconnected data.
   2. They are very useful in applications like social networks and recommendation engines.
   3. Examples: Neo4j, Amazon Neptune.
   4. Common use cases:
      1. Social Networks: Storing and analyzing relationships between users, such as friendships, followers, and interactions.
      2. Recommendation Systems: Analyzing user preferences and behaviors to provide personalized recommendations based on connections and similarities.
      3. Fraud Detection: Identifying suspicious patterns and relationships in financial transactions or user activities.
5. **In-Memory Databases**:
    1. In-memory databases store data primarily in the main memory (RAM) rather than on disk, allowing for extremely fast data access and processing.
    2. They are ideal for applications requiring real-time data processing and low-latency access.
    3. Examples: Redis, Memcached, Apache Ignite.
    4. Common use cases:
        1. Caching: Storing frequently accessed data in memory to reduce latency and improve application performance.
        2. Real-time Analytics: Processing large volumes of data in real-time for analytics, monitoring, or event processing.
        3. Session Management: Managing user sessions in web applications for quick access to session data.
