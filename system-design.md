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

