1. We know that there are in-memory databases and Disk based databases but it is Important to know clearly what is the advantages of in-memory databases other than simply providing faster access to the Data:

### In-Memory DB:
	1. Faster Access because this is in RAM but this is a volatile memory (on a system restart the data is lost)
### Durability of in-Memory DB:
- But to counter this a special type of recovery log system is used like (WAL) (write ahead log) here logs are stored in a disk.
- **Purpose and Maintenance**: The backup copy is a disk-based, sorted structure used for recovery by combining it with log records. Updates to the backup are asynchronous and processed in batches to minimize I/O overhead, ensuring client operations are not blocked.
- **Checkpointing and Recovery**: Through checkpointing, log records are periodically applied to the backup, creating a consistent snapshot and allowing old logs to be discarded. During recovery, the database is restored by loading the backup and replaying recent log entries for the latest state.
### Data-structure drama  in-Memory 
Disk-based databases use specialized storage structures, optimized for disk access. In memory, pointers can be followed comparatively quickly, and random memory access is significantly faster than the random disk access. Disk-based storage structures often have a form of wide and short trees (see “Trees for Disk-Based Storage”), while memory-based implementations can choose from a larger pool of data structures and perform optimizations that would otherwise be impossible or difficult to implement on disk [MOLINA92]. Similarly, handling variable-size data on
disk requires special attention, while in memory it’s often a matter of referencing the value with a pointer.

