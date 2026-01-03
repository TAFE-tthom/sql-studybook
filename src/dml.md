# Inserting, Updating and Deleting

DML segment is focused on manipulation of data within the schema itself. It is one thing to be able to queyr the data but we need to be able to change it and add and remove data from our database.

## Insert

One of the most important statements, we need to be able to insert data into our tables.

Assuming we were adding a new Product to a `Product` table

```sql
INSERT INTO Products (ProductName, SupplierID, CategoryId, Quantity, UnitPrice, UnitsInStock, UnitsOnOrder, ReorderLevel, discontinued) 
VALUES('Super Soda', 30, 2, 5, 2, 10, 2, 5, FALSE);

```

### Multi-Insert

We can insert multiple entries within the same statement as well.

```sql
INSERT INTO Products (ProductName, SupplierID, CategoryId, Quantity, UnitPrice, 
UnitsInStock, UnitsOnOrder, ReorderLevel, discontinued) 
VALUES
('Super Soda', 30, 2, 5, 2, 10, 2, 5, FALSE),
('Bad Cola', 30, 2, 7, 2, 10, 2, 5, TRUE),
('Old Bread', 30, 7, 7 2, 10, 2, 5, TRUE),
('Cake', 30, 3, 5, 2, 10, 2, 5, FALSE),
('Ice Cream', 30, 3, 5, 2, 10, 2, 5, FALSE),

```

## Update

Update statements typically involve setting a value for a particular column and a where clause (unless you want to set it for the whole table).

Lets go through the following example:

```sql
UPDATE People
SET FirstName = 'Jeff'
WHERE FirstName = 'Jeffrey'
```

We find all entries where the FirstName is `'Jeffrey'` and set the value to `'Jeff'`. Normally we set individual records using a primary key and searching for it.


## Delete

The purpose of delete is fairly straight forward, we want to remove entries from a table.

```sql
DELETE FROM Product
WHERE ProductID = 1; 
```

Given the ProductID, we are able to remove this product from the table. Similar to Update and Selected, the where clause supports most of the typical operations.

**CAREFUL!** We have specified a `WHERE` clause in our statement, make sure you include this with your `DELETE` statement otherwise you might end up not having a good time.


## Loading Data

MySQL/MariaDB has its own specifics around loading data from files and other data sources. 

```sql
LOAD DATA INFILE 'data.csv' INTO TABLE Person
  FIELDS TERMINATED BY ',';
```

* 'data.csv' is a file that is local to the server. You can use relative and absolute paths with this command.

* It is common to handle files which may have different separators and patterns. In this case, a .csv is a file of comma separated values. Typically usable in spreadsheet software.

**Caution!** You need to be mindful about how the file was saved. It is very easy to not observe this and most systems will expect **unix line-feed** rather than **windows line-feed**. This is a difference between a single character (`\n`) and two characters (`\r\n`).

You can inspect the file and observe the difference using a tool like `xxd` or use a tool called `dos2unix` which will convert the line feed endings to unix ones. 


