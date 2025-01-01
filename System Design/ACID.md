### Atomicity
Either the The operation Should happen Completely or it should not there shouldn't be anything in between to ensure that we can nicely wrap the operations in a Transaction
	My Own Experience
	 1. When i Was creating the signup Endpoint I had Take User address as an Input and also User Details as an Input
    2. In the Database I had address table separately and the users table separately I had to enter details into both of them atomically So I wrapped both of them in a transaction and executed it.
Implementation of Atomicity:


### Consistency
- When I have a Foreign key in the Table Corresponding Information Should be present in the other table where the primary key is this key.
- If i have 100 dollars i should not be able to transfer 200 dollars

No matter what happens my database moves from one consistent state to other consistent state
Ex:
Lear about `constraints` `cascades` `triggers`
`CASCADES`:
	1. For example i have a parent table `user` and i have an `address` table as child so if i delete `user` table the `address` table will become orphan so what will `cascades` do is that they will also remove all address related to that particular user
	2. Parent row delete all the child tables also delete
`Trigger`:
		1. On certain operation trigger something
### Isolation Levels
- Its not like at a single time Instance only one transaction is happening in the database, their may be multiple transactions that are happening in the database  so the isolation levels are nothing but How much of one transaction is visible to the other transaction before the second one first one commits.
- ![[Pasted image 20241027231515.png]]
- Typically there if it perfectly not visible then the transactions happen serially this is something that we can configure
### Further More at [[Isolation Levels]]

### Durability

No matter what happens so long as disc is there data should be there.
the changes should outlive the outage.
SQL databases are atmost Durable 


Implementation of Atomicity