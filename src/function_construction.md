# Using Functions

Functions within SQL operate similar to other programming languages. The structure of a function is composed of the following components.

* Function Name/Symbol
* Parameters (0 to many)
* Body of the function
* Return Value (if specified)

Every function has to have a name in which it can be referred by. Without this, we cannot refer to it within out queries or describe it succinctly. Importantly, a function can have between 0 to many parameters. Each parameter represents an object that is to be typically used within the body of the function. Arguments are usually given to the function when it is called.

Each function has a body in which is specifies the instructions to execute. This body can range between 0 to many lines of SQL code in which it can also call other functions.

The return value of a function which is common for functions that operate within queries, typically is the final value or computed value (usually the intent of the function).

## Common Builtin Functions

SQL supplies you with a large number of builtin functions that you can utilise within your queries. While it is very feasible to reimplement the functionality for yourself. It is useful to use the existing common scalar functions.

* `CONCAT` - Concatenates two or more strings into one, similar to `+` in JS and C#

* `FORMAT` - Format string function, uses identifiers and formats the value to be part of the string.

* `IIF` - Allows the query to make decisions within the query itself.

* `LOWER` and `UPPER` - Changes the case of the string, turns it either all lower case or all upper case.

* `DATEDIFF` - Gets the differences between days. In addition, you likely want to use `DAYOFWEEK`, `DAYOFMONTH` and `DAYNAME` to extract details from the date you had been given.

## Usage within a query

You can use a builtin function within a query in multiple places. Commonly, you will use it with columns or within the `WHERE` clause. In the example below, you demonstrate using `CONCAT` with `LastName` and `Firstname`.

```sql
SELECT ID, Company AS [Company Name], 
    CONCAT([LastName], ', ', [FirstName]) AS [Contact Person]
FROM Customers;
```

### Making decisions with queries

We may want to categorise and compute a column during a query. This is where we need to use `IIF`. Let's construct a query that utilises this.

```sql
SELECT ProductName, available_qty, price,
  IIF(available_qty > 0, 'In-Stock', 'Unavailable') AS InStockStatus
  FROM Product;
```

The `IIF` function allows you to input a boolean expression as the first argument, given the outcome of that expression for each row, the final output will either conclude that the Product is `In-Stock` or `Unavailable`.

The above expression can be rewritten to use `CASE`, `WHEN` and `ELSE` operators.

```sql

SELECT ProductName, available_qty, price,
  CASE WHEN available_qty > 0
    THEN 'In-Stock'
    ELSE 'Unavailable'
  END
  AS InStockStatus
  FROM Product;
```

The above snippet is an expansion of the function if we were to decompose it into just its body.
