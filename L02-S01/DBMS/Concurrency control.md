
## Concurrency Control

- Transaction schedule
		is the ordering of the operations of a transaction based on time
- Serial and Non-serial schedules
		- Serial: schedule A and B
				for every transaction T participating in the schedule, all the operations of T are executed consecutively in the schedule. (transactions are executed one after the other with no interleaving)
		- Non-serial: shedule C and D
				otherwise
		![[serial_non-serial.jpg]]

- Conflicting operations in a schedule:
		- they belong to two transactions
		- access the same database item
		-  atleast one of them is a write

- Equivalence
		- result Equivalent: both schedules produce the same final state of the database
		- conflict Equivalent: the order of any two confilicting operations is the same in both schedules
		
- Serializability of a schedule:
		A schedule S of n transactions is serializable if it is equivalent to some serial schedule of the same n transactions.
			Ex: schedule D is equivalent(conflict) to schedule A. Therefore D is serializable
					schedule C is not equivalent to any of the two serial schedules A and B

- Testing for conflict serializability of a schedule
		- Draw a precedence graph. If no cycles persent, the schedule is serializable(conflict)
		- Node for each transaction
		- arrow for two conflicing operations(according to order. from the 1st to 2nd)
	![[precedenceGraph.jpg]]


### Locking Techniques

- Read/ Write locks
		- Read lock/Shared Lock:(lock-S)
				No write operations allowed. Multiple reads allowed on the item for other transactions.
		- Write Lock/Exclusive Lock:(lock-X)
				Other transactions cannot read or write the locked item. Access exclusive for the locked transaction
- Read/ Write locking guidelines,
		- read lock before reading
		- write lock before writing
- Read/ Write locks alone doesn't ensure serializability

##### Two-Phase Locking
- A protocol to follow with read/write locks that ensures serializability of the schedule
- Two phases
		1. Growing or Expanding phase
				Locking items and upgrading locks(read lock to write lock). No releasing locks.
		2. Shrinking phase
				Unlocking items and downgrading locks(write lock to read lock). No obtaining locks.
- Problems caused by locking techniques
		- Deadlocks:
				when each transaction T in a set of two or more transactions is waiting for some item that is locked by some other transaction T' in the set. Hence, each transaction in the set is on a wating queue, waiting for one of the other transactions in the set to release the lock on an item.
								  ![[deadlockexample.jpg]] 
		- Starvation
				
				

- Deadlock prevention algorithms:
	Older transactions have low timestamps compared to youger ones.
	Assume Ti tries to lock an item X but not able to, because another transaction Tj is holding the item with an incompatible lock,
	- lock all the items it needs in advance. if any of the items cannot be obtained, none of the items are locked. Rather, the transaction waits and then tries again to lock all the items it needs.(not practical)
	- Wait-die scheme:
				If Ti=older --> wait
				else if Ti=younger --> die(restart later with the same timestamp)
	- Wound-Wait scheme:
				If Ti=older --> Wound Tj(abort Tj and restart later with same timestamp)
				else if Ti=younger --> wait
		(in both cases, a younger transaction is aborted)
		
