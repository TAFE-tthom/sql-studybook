# Transactions, Stored Procedures and Functions

Within this chapter we will be examining transactions, stored procedures and functions (user defined functions). By default with SQL implementations, each statement/query are usually treated as transaction by themselves. You are able to modify this behaviour as a way to control the granularity of the operations.

In conjunction with transactions, this chapter explores constructing stored procedures and user defined functions. These constructs can use transactions within them and provide a resuable set of code of which databases can leverage.


We will be exploring the current topic areas.

* Variables
* Transactions, Commits and Rollbacks
* Grouping operations and ACID
* Stored Procedures
* User-Defined Functions

## Variables

Like other programming languages, SQL also has variables in which the user can leverage. These commonly get used within stored procedures and functions but can be used within most SQL queries.

To declare a variable, you will need to use the `@` prefix and the `SET` keyword.  

```sql
SET @hello = 'Hello Variable';
```

You are able to use the value within a `SELECT` statement and other parts of SQL for your own purposes.

```sql
SET @userid = 10;

-- Using @userid in `WHERE`
SELECT * FROM User WHERE user_id = @userid;
```
