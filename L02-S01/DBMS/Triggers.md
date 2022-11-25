<u>Trigger Types</u>
- DDL
- DML
	- after Trigger: Trigger run after the operation
	- before Trigger: Trigger run before the operation
	- instead-of Trigger: Trigger run instead of the opertion
- CLR
- Logon 

### DML Triggers

- When running insert, delete, update operations in MSSQL server, tempory tables named,
	- "inserted" 
	- "deleted" 
	would be created and deleted  at each transaction. We can only access these tables using triggers.
```
CREATE TRIGGER pa1 
ON Product
AFTER UPDATE
AS
BEGIN
		DECLARE @qtyAvl INT
		DECLARE @rol INT
		DECLARE @PNo VARCHAR(6)
		SELECT @PNo=productNo, @qtyAvl=qty_Available, @rol=re_order_level FROM inserted
		IF @qtyAvl<=@rol
		BEGIN
			DECLARE @maxNoteNo INT;
			SELECT @maxNoteNo=MAX(NoticeNo) FROM Items_to_Order;
			INSERT INTO Product Items_to_Order VALUES(@maxNoteNo,@PNo,GETDATE());		
		END
END
```