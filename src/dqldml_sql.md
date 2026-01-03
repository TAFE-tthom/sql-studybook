# Querying and Manipulation

We have seen `select` and `insert` keywords already but we will be revisiting them as there is more to these statements that we can use and combine with.

We have separate terms, last session we introduced 'DDL' which stood for Data Definition Language which is concerned about the modelling and structuring of a database via the SQL language.

## DQL - `SELECT`

You are able to retrieve elements from a table (and multiple tables) using the `SELECT` keyword.

Format:
```sql
SELECT [columns] FROM [tables]
```

There is also a wildcard symbol that allows the query to include all columns from a table ( `*` ).



### Multi-Columns

You re able to specify multiple columns within SQL or even multiple pieces of data. When using a `SELECT` statement, you should separate each piece using a comma (,).

Example:

```sql
SELECT 'Ricky', 'Davidson';
```

We can observe the data being separated by a comma.

To expand on this, when using a tabling, we are refer to the table's columns within the select statement.

```sql
SELECT isbn, title, author FROM Book;
```

The above query outlines that the `isbn`, `title` and `author` columns will be included in the query.

### DQL and Built-In Functions

However, lets start using some built-in functions within a query.

We will use the `CONCAT` function that allows us to merge two fields and represent it as a single column in the final results.

```sql
SELECT ID, Company AS [Company Name], 
    CONCAT([LastName], ', ', [FirstName]) AS [Contact Person]
FROM Customers;
```

We can also specify the column name of these generated columns. The `AS` keyword is usable within this context.


### Aliasing with `AS`

We can use the AS keyword after specifying the column name to give it another name. SELECT 'Hello' as Greeting;

It will show Greeting as the column name and 'Hello' one of the entries below.

A real world example would look like this.

```sql
SELECT CONCAT(first_name, ' ',
  last_name) AS Fullname
  FROM Customer;
```

This will output fist_name and last_name, separated by a space under a single column called Fullname.

The `AS` keyword is used as a way to give a column or result from an operation another name (alias). This is helpful if we want to have a shorthand for columns or tables.

```sql
SELECT C.ID, Company AS [Company Name] FROM Customers AS C;
```

In the above sample, we can observe how the keyword is applied here.



