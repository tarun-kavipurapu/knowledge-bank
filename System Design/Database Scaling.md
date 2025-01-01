### There are two things we need to be aware of to scale the database

- Read-heavy Traffic
    - following-power law(use caching for most used endpoints)
    - not following
- Write-heavy traffic

## Read Heavy Traffic

Two options

- Read Replica
    
    - We create a Read replica where all the reads of the the traffic will be diverted
    - It is nothing but creating another database instance which is only used for database reads
    - This logic has to be managed in the API level where we have two connection objects one for replica and another for write database. and we do all the reads with replica connection object
    
    Acheiving Consistance when write is happening in the database:
    
    1. when ever a write happens this should be simultaneously updated in the read replica this can be done in two ways:
        1. Synchronously: The entire API will wait till the write in the Read Replica is done this will increase latency but ensure strong consistency
        2. ![[image.png]]
	1. b. Asynchronously: Eventual Consitency
		1. Replica Pulls data consistently
			![[image(1).png]]

## Write Heavy Traffic

Sharding is the solution for this

We divide the data in the database into mutually exclusive subsets of data with a key as a property and

API can take care of the routing logic
![[image(2).png]]