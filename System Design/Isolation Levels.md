Try to do this practically 
---

### **ACID - Isolation Levels**

### Practical Implementation of this is already done
- **in ACID represents Isolation**, which defines how much of one transaction is visible to another. We can configure this visibility using different isolation levels. Below, we’ll look at each isolation level with practical examples.
  
  **Note**: The two transactions discussed are happening in parallel (simultaneously). You need to practically perform them to fully understand their behavior.

### **Standard SQL Isolation Levels**

	1. ### Repeatable Reads
   - **Description**: In the Repeatable Reads isolation level, once a transaction reads data, it will always get the same consistent value throughout the transaction, even if other transactions modify the data and commit.
   - **Key Behavior**: No matter what changes occur, consistent reads are maintained within the same transaction.

   **Example**:
   - **Transaction 1**: Reads `Account A` balance as $1000.
   - **Transaction 2**: Updates `Account A` balance to $500 and commits.
   - **Transaction 1** (later in the same transaction): Reads `Account A` balance again, still getting $1000, despite the changes committed by Transaction 2.
   
   **Use Case**: Situations requiring consistent reads during a transaction, such as generating a report or performing calculations without data inconsistencies.

2. ### **Read Committed**
   - **Description**: In the Read Committed isolation level, each read operation within a transaction sees the latest committed data. This level prevents dirty reads but allows **non-repeatable reads**, as data can change if other transactions commit.
   - **Key Behavior**: Reads always get the freshest data after other transactions commit changes.

   **Example**:
   - **Transaction 1**: Reads `Account A` balance as $1000.
   - **Transaction 2**: Updates `Account A` balance to $500 and commits.
   - **Transaction 1** (later in the same transaction): Reads `Account A` balance again and gets the updated $500.
   
   **Use Case**: Standard web applications where data accuracy is necessary, but some changes in read values are acceptable.

3. ### **Read Uncommitted**
   - **Description**: The Read Uncommitted isolation level allows transactions to read data that other transactions have not yet committed. This can lead to **dirty reads**, where data that might be rolled back is visible to other transactions.
   - **Key Behavior**: No locks are placed, allowing maximum concurrency at the expense of data consistency.
   
   **Example**:
   - **Transaction 1**: Updates `Account A` balance from $1000 to $500 (but hasn't committed yet).
   - **Transaction 2**: Reads `Account A` balance as $500 (even though Transaction 1 hasn’t committed).
   - If **Transaction 1** rolls back, **Transaction 2** will have read incorrect data.
   
   **Use Case**: Suitable for low-priority background operations where maximum concurrency is needed and data accuracy isn't critical.

		
4 . ### **Serializable**
   - **Description**: The Serializable isolation level is the strictest, ensuring that transactions are executed as if they were run sequentially. This prevents dirty reads, non-repeatable reads, and phantom reads, ensuring complete isolation between transactions.
   - **Key Behavior**: Transactions are fully isolated, and data is locked to prevent conflicts, leading to the highest level of consistency but with reduced concurrency.
   
   **Example**:
   - **Transaction 1**: Reads all rows with a balance greater than $1000.
   - **Transaction 2**: Tries to update or insert data that matches the criteria of Transaction 1 but must wait until Transaction 1 completes.
   - Transaction 2 will not even move forward util transaction 1 is committed or rolled back
   - **Transaction 1** finishes, then Transaction 2 proceeds, ensuring no data conflicts.
   
   **Use Case**: Critical systems like financial applications, inventory management, or scenarios requiring strict data consistency.

### **Summary Table of Isolation Levels**

| Isolation Level  | Dirty Read | Non-Repeatable Read | Phantom Read |
| ---------------- | ---------- | ------------------- | ------------ |
| Read Uncommitted | Yes        | Yes                 | Yes          |
| Read Committed   | No         | Yes                 | Yes          |
| Repeatable Read  | No         | No                  | Yes          |
| Serializable     | No         | No                  | No           |

---

