

## Views

- Simply, to create a view,
	`CREATE VIEW View_name AS (SQL STATEMENT);`
- Views can contain computed columns. Otherwise, they act like normal tables. They can be updated also. 
- SQL server doesn't support updating multiple base tables at once via views. But single base table updation is possible. This is true for insertion as well.
- From MySQL documentation:
		"For a view to be updatable, there must be a one-to-one relationship between the rows in the view and the rows in the underlying table."
- `WITH CHECK OPTION` : if updated or inserted records becomes hidden from the view, this option will deny the operation.
```
CREATE VIEW mytestview3  
AS  
SELECT c.clientNo,c.name,c.city,s.Sales_Order_No,s.Sales_Order_Date,s.Delivery_Address  
FROM client c, Sales_Order s  
WHERE c.clientNo=s.ClientNo AND Sales_Order_Date>'01-May-2010'  
WITH CHECK OPTION
```

## Stored Procedures


### MS SQL Server

- In MS SQL server, 
		- <mark>All</mark> variables are started with @ sign

- Procedure creation syntax
```
DELIMITER //

CREATE PROCEDURE getQuantity(@pno VARCHAR(6) IN, @qty INT OUT)
AS
BEGIN
		SELECT @qty=qty_available FROM product p WHERE productNo=@pno;
END //

DELIMITER ;
```
- To call the procedure
```
DECLARE @QNTY INT;
EXEC GetQuantity('p0001', @QNTY OUT);
PRINT @QNTY;
```

- If statement
```
IF NOT EXISTS (SELECT * FROM Client WHERE ClientNo='C4')
BEGIN
	INSERT INTO Client Values('C4', '0728428482');
END
```

#### MYSQL server

- Types of Variables in MYSQL
		- User defined Variables
				- no prefix
				- session specific(a user variable defined by one client cannot be seen or used by other clients)
 		- Local Variables
		 		- start with @
		- Global Vairables 
				- starts with @@
https://stackoverflow.com/questions/11754781/how-to-declare-a-variable-in-mysql

- Procedure Creation syntax
```

-- local variables used
CREATE PROCEDURE getQuantity(IN pno VARCHAR(6), OUT qty INT)
BEGIN
	SET qty=(SELECT qty_available FROM product p WHERE productNo=pno);
END //

DELIMITER ;
```

- To call the procedure
```
-- user variables
CALL getQuantity('p0001', @Qty);
SELECT @Qty ;

```

- If statement
```
IF NOT EXISTS (SELECT * FROM Client WHERE ClientNo='C4') THEN
	INSERT INTO Client Values('C4', '0728428482');
END IF
```

### Common
- Stored procedures can only return INT values. So, as an alternative we can specify an output variable
- We can set the delimiter as,(to avoid executing the statement in the middle of defining the procedure)
		`DELIMITER //`
		`DELIMITER ;`
