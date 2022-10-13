## Priming

- RDBMS normal operating procedure

(scanning, parsing, validating) -> (Query optimizor) -> execution strategies -> (code generator) -> code to execute queries -> (Runtime DB processsor) -> execute

- Query Optimizor just comes up with a reasonable execution strategy.



## Important Points when calculating the I/O cost of a query
- Total cost of a step = Input cost + Output Cost
- output cost of the last step is always 0
- Can't keep part of the table in the memory. Either the whole thing on memory or on disk cache
- Query Optimizor in a relational DBMS![[query optimization workings.jpg]]

- [[Tutorial 06 - Query Optimization.pdf]]  and answers at.
<iframe src="https://miro.com/app/live-embed/uXjVPdmZ2Rw=/?moveToViewport=-600,3952,2553,15839&embedId=546199016559" scrolling="no" allowfullscreen width="900" height="600" frameborder="0"></iframe>



