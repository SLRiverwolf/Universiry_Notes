- Clustered Index:
	- Clustered indexes sort and store the data rows in the table or view based on their key values
	- One table can only contain one clustered index(but could cotain a 1 index based on multiple fields)
	- Searching is fast
	-  insertion is slow
- Non-clustered Index:
	- Nonclustered indexes have a structure separate from the data rows. A nonclustered index contains the nonclustered index key values and each key value entry has a pointer to the data row that contains the key value.
	- searching is slow
	- insertion is fast

- When we are creating a table with a primary key in MS SQL, a clustered index will be automatically created based on the P.K
- We can create an index on a table using the GUI of the management studio or,
`CREATE CLUSTERED INDEX idx_ISBN ON Book(ISBN);`



<iframe width="1000" height="1000" src="https://learn.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described?view=sql-server-ver16"></iframe>




#### From the Text Book

If records of a file are physically ordered on a nonkey field(not unique) that field is called the <b>clustering field</b>.
![[clusteringIndex.jpg]]

- another nondense/sparse index type