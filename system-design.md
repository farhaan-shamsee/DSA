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
