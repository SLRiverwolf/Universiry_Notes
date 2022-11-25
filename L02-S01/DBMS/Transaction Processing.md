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



## Lab session

- 3 Modes of operation in microsoft sql server,
			1. AutoCommit transaction
			2. Implicit transaction
			3. Explicit transaction

#### Explicit Mode

- Trasanctions must be commited, rolledback manually
- Basic syntax of a transaction in microsoft sql server
```
BEGIN TRANSACTION  
UPDATE account set Balance=balance-10000 where AccNo=100  
if @@Error!=0 GOTO MyErrorHanddle  
UPDATE account set Balance=balance+10000 where AccNo=101  
if @@Error!=0 GOTO MyErrorHanddle  
COMMIT TRANSACTION  
RETURN  

MyErrorHanddle:  
ROLLBACK TRANSACTION
	
```
			
- `@@Error` variable:
		- stores the status of the last <mark>statement</mark>. 0 if no errors otherwise there was an error
		- gets overwritten after the next statement execution. So each statement must be checked individually and rolled back.
		- Doesn't catch the record does'nt exist error
			Ex: `UPDATE account set Balance=balance-10000 where AccNo=100`
			`@@Error` is still `0` even if there's no account with AccNo 100.
			So, `@@ROWCOUNT` is a better alternative(if there's an error in the statement, affected rows is 0.)
			Ex:
```
BEGIN TRANSACTION  
UPDATE account set Balance=balance-10000 where AccNo=101  
if @@ROWCOUNT=0 GOTO MyErrorHanddle  
UPDATE account set Balance=balance+10000 where AccNo=102  
if @@ROWCOUNT=0 GOTO MyErrorHanddle  
COMMIT TRANSACTION  
RETURN  
MyErrorHanddle:  
ROLLBACK TRANSACTION
```