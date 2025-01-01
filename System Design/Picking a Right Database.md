It is not that NOSQL are scalable and SQL are nonscalabel the things that make Nosql scalable are their ability to shard easily we can also achieve this by make out sql database:

Why NOSQL db scale:

1. There are no realations and constraions
2. data is modelled to be sharded(split across multiple servers)

if we relax the above conditions on relational DB we can scale it too..

- Drop foreign key checks
- Do not use cross shard transactions
- Do manual sharding

Criteria to select which database to scale:

1. Understand what data are you storing are they stored in relations or do they have constraints
2. Understand how much of data we will be acessing
3. What kind of queries we will be needing
4. Any special features to expect:
    1. Example:Expiration

We can Make the Permutation and combination of above criteria and choose the database.

1. If data can fit on a single node and we need strong consistency & data correctness we need to go **with relational DB**
    
2. If data can fit on a single node and we need aggregations **with relational DB**
    
3. If we need fast KV access—>go for Redis
    
4. if we need advanced data-structure go with redis
    

if data does not fit with one node

- an we have expertiese in SQL and can do manual sharding
    - drop the constraints and go for relational db
- if we have simple KV access
    - go for KV store like Dyanmo DB, mongoDB,etc
- If we need Graph algorithms
    - go for graph DB like Neo4j.

When you need **high ACID compliance** and **high scalability**, the solution typically involves choosing a database that balances strong consistency with scalability, or implementing hybrid architectures to meet both requirements. Here are strategies and options:

---

### **1. Use Distributed SQL Databases**

Distributed SQL databases are designed to combine **ACID compliance** with horizontal scalability. These databases distribute data across multiple nodes but maintain strict transactional guarantees.

### **Examples**:

- **CockroachDB**:
    - Strong consistency and fault tolerance.
    - Automatically shards data across nodes for scalability.
- **Google Spanner**:
    - A globally distributed SQL database with strong ACID guarantees.
    - Ideal for applications requiring global consistency.
- **YugabyteDB**:
    - Open-source distributed SQL database optimized for multi-cloud setups.

### **Use Case**:

- Applications like global financial systems, e-commerce, or real-time analytics requiring ACID compliance and distributed data.

---

### **2. Partitioning and Sharding**

Partitioning and sharding involve splitting data across multiple servers (or nodes) to improve scalability while still using an SQL database.

- **Horizontal Partitioning (Sharding)**:
    - Data is split based on keys (e.g., customer IDs or regions).
    - Each shard functions as an independent database, maintaining its own ACID guarantees.
- **Challenges**:
    - Implementing cross-shard transactions can be complex.
    - Often requires middleware or a database that natively supports sharding (e.g., MySQL Cluster).

---

### **3. Leverage Multi-Model Databases**

Multi-model databases provide support for multiple data models (e.g., relational, document, key-value) within a single system. These databases can achieve scalability while supporting ACID transactions.

### **Example**:

- **Azure Cosmos DB**:
    - Offers support for multiple consistency levels (strong to eventual).
    - Can maintain ACID transactions within a partition while scaling globally.

---

### **4. Use a Hybrid Approach**

Combine SQL and NoSQL databases to handle different parts of your application. For example:

- Use an **SQL database** for transactions requiring ACID compliance (e.g., order processing).
- Use a **NoSQL database** for scalable, non-transactional workloads (e.g., user session storage, analytics).

### **How It Works**:

- Maintain a reliable SQL database (e.g., PostgreSQL) for core operations.
- Offload high-traffic read-heavy operations to a caching layer (e.g., Redis) or a NoSQL database.

---

### **5. Optimize with Middleware**

Middleware solutions like **Two-Phase Commit** or **Distributed Consensus Algorithms** (e.g., Paxos, Raft) can ensure ACID compliance across distributed nodes.

### **Example**:

- Use a system like **etcd** or **Zookeeper** to manage distributed consensus for critical transactions.
- Pair with databases that allow distributed transactions (e.g., PostgreSQL with distributed extensions like Citus).

---

### **6. Advanced Techniques**

- **Event Sourcing and CQRS (Command Query Responsibility Segregation)**:
    - Use event sourcing to maintain a log of all transactions (ACID-compliant SQL) and allow NoSQL for query optimization.
- **Materialized Views**:
    - Create materialized views in a relational database to serve queries faster while maintaining ACID compliance.

---

### **Summary of Options**

|Requirement|Solution|
|---|---|
|Globally distributed with ACID compliance|Google Spanner, CockroachDB|
|Scalable SQL with sharding|MySQL Cluster, PostgreSQL with Citus|
|Multi-model and distributed data|Azure Cosmos DB, YugabyteDB|
|Hybrid ACID and NoSQL architecture|SQL (PostgreSQL) + NoSQL (Redis, MongoDB)|
|Custom ACID-compliant distributed system|Two-Phase Commit, Paxos, Raft|

Choosing the right approach depends on your system's specific needs, such as latency tolerance, global distribution, or complexity of transactions. For high ACID and scalability, **distributed SQL databases** like CockroachDB or Google Spanner are often the best choices.