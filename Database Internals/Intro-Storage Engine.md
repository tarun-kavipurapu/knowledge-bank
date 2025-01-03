Theese Notes are Based on Database Internals book
Database Managment Systems (lets call it database in future ) can be broken down into 4 layers

1. **Transport Layer**: Handling connections with the clients
2. **Query Optimization layer**: Optimization of the Queries for the better response time
3. **Execution Layer**:Executes the queries 
4. **Storage Layer**:Handles the storage of the data

The storage engine (or database engine) is a software component of a database management system responsible for storing, retrieving, and managing data in memory and on disk, designed to capture a persistent, long-term memory of each node

- A particular Database system may be compatible with many storage Engines and each of them may be used according to the specifications of the application required
	- Example: MYSQL can be used for InnoDB,RocksDb,MyISAM
 - MySQL **supports multiple storage engines**, but this does not mean that MySQL uses all of them simultaneously for the same tables or operations. Instead, **you can choose the storage engine for each table individually**, depending on the use case and the features you nee
**Picking a Right Database:** Database is a Longterm decision it is important to pick it wisely some of the points or considerations while picking:
1. Try to emulate the upper bound workload that you may encounter in your application and measure which database is working best for you in that senario and make decision according to the measured aspects.
2. To compare databases, it’s helpful to understand the use case in great detail and define the current and anticipated variables, such as:
	1. Schema and record sizes  
	2. Number of clients
	3. Types of queries and access patterns  
	4. Rates of the read and write queries Expected changes in any of these variables
3.  Knowing these variables can help to answer the following questions: 
	1. Does the database support the required queries?
	2. Is this database able to handle the amount of data we’re planning to store?
	3. How many read and write operations can a single node handle? How many nodes should the system have?  
	4. How do we expand the cluster given the expected growth rate? What is the maintenance process?
4. Most databases already have stress tools that can be used to reconstruct specific use cases. If there’s no standard stress tool to generate realistic randomized workloads in the database ecosystem, it might be a red flag. If something prevents you from using default tools, you can try one of the existing general-purpose tools, or implement one from scratch.



Part I. Understanding Trade-Offs

- As users, we can see how databases behave under different conditions, but when working on databases, we have to make choices that influence this behavior directly.

- Designing a storage engine is definitely more complicated than just implementing a textbook data structure: there are many details and edge cases that are hard to get right from the start. We need to design the physical data layout and organize pointers, decide on the serialization format, understand how data is going to be garbage-collected, how the storage engine fits into the semantics of the database system as a whole, figure out how to make it work in a concurrent environment, and, finally, make sure we never lose any data, under any circumstances.

- Not only there are many things to decide upon, but most of these decisions involve trade-offs. For example, if we save records in the order they were inserted into the database, we can store them quicker, but if we retrieve them in their lexicographical order, we have to re-sort them before returning results to the client. As you will see throughout this book, there are many different approaches to storage engine design, and every implementation has its own upsides and downsides.

- When looking at different storage engines, we discuss their benefits and shortcomings. If there was an absolutely optimal storage engine for every conceivable use case, everyone would just use it. But since it does not exist, we need to choose wisely, based on the workloads and use cases we’re trying to facilitate.

- There are many storage engines, using all sorts of data structures, implemented in different languages, ranging from low-level ones, such as C, to high-level ones, such as Java. All storage engines face the same challenges and constraints. To draw a parallel with city planning, it is possible to build a city for a specific population and choose to build up or build out. In both cases, the same number of people will fit into the city, but these approaches lead to radically different lifestyles. When building the city up, people live in apartments and population density is likely to lead to more traffic in a smaller area; in a more spread-out city, people are more likely to live in houses, but commuting will require covering larger distances.












