# Transaction Processing

- Concurrency Problems in DBMS
		-   Temporary Update Problem
		-   Incorrect Summary Problem
		-   Lost Update Problem
		-   Unrepeatable Read Problem
		-   Phantom Read Problem
<iframe src="https://www.geeksforgeeks.org/concurrency-problems-in-dbms-transactions/" scrolling="no" allowfullscreen width="900" height="600" frameborder="0"></iframe>


- Transaction concept:
		- atomic unit, either completely done or not done anything
- Properties of a transaction: ACID principle
		- Atomicity: 
				A transaction is an atomic unit of processing: it is either performed in its entirety or not perfomed at all
		- Consistency preservation
				A transaction is consistency preserving if it complete execution takes the database from one consistent state to another
		- Isolation 
				The execution of a transaction should not be interfered by anyother transaction occuring concurrently
		- Durability or permanency
				the changes applied to the database by a committed transaction must persist in the database.
				