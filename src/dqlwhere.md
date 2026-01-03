# Querying and Filtering

## `WHERE` clause

A very common keyword is using the WHERE keyword that allows you to filter data. This is critical to most sql usage as we are usually wanting to retrieve records that contain certain properties.

You can constrain and search for a particular entries and leverage certain predicates for specific columns.

```sql
SELECT *
FROM Employees
WHERE ID >= 4 AND ID <= 9;

```

We are retrieving all employees that have an ID between 4 and 9.

### Operators

To use the WHERE clause, we will also need to introduce common operators that are used for comparison.

The format of the query takes on the following:

```sql
SELECT columns,... FROM tables,...
  WHERE column OPERATOR value
```

OPERATOR and value are placeholder words in this case and are not part of the

* OPERATOR can mean the following:
  * = and == - Checking to see if it matches the value on the right handside `WHERE amount == 5`;
    or
    `WHERE name = 'John'``;

  Commonly = is used, == does appear in most sql vendors but double check the manual.
    * != - Used to check if the row value does not equal the value being checked. `WHERE amount != 10`;

    * >, <, <=, >= - These are used to check if a numeric or date column (or value) on the right handside.
    ```sql
    WHERE date_paid
        >= '2020-12-01 00:00:00';
    ````
It is possible to have multiple conditions within a query using OR and AND.

```sql
WHERE amount = 5 OR amount = 10;
```

The above snippet will have a clause that checks if the amount if 5 OR 10.

With AND, we need both conditions to be true.

```sql
WHERE name = 'John' AND id = 10;
```

It will check if the name is John and that their id is 10.

## `WHERE` examples

You can constrain and search for a particular entries and leverage certain predicates for specific columns.

```sql
SELECT *
FROM Employees
WHERE ID >= 4 AND ID <= 9;

```

We are retrieving all employees that have an ID between 4 and 9.

Negation of the field can be used to exclude a entries from our final results.

```sql
SELECT *
FROM Customers
WHERE ID != 4;
```
This can also take the form exclude a set or range of data.


```sql
SELECT *
FROM Employees
WHERE NOT (ID >= 4 AND ID <= 7);
```

This can be expanded to other datatypes which will have their own semantics on operator usage. Please review the resource 8 at the end of this slide-deck.

