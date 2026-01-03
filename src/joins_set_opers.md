# Unions, Intersection and Difference

We start venturing into some interesting set operations. As a note, it is best to view these tables as **sets** as it maps nicely to set operations in mathematics.

## Unions

Unions allow you to merge the results of two queries into a single result set.

This takes all records in table A and adds it to all records with table B. You will typically use unions as a way to finding similarly named tables and using these fields to produce a result set that is uniform.

```sql
SELECT firstname, lastname, address FROM customers
UNION
SELECT firstname, lastname, address FROM employees;
```

* Getting contact details for customers and employees
* Retrieving name and phone numbers for companies and individuals

It can be occasionally difficult to identify when and where you will use unions but they are likely more powerful when we start working with more complex data or data a subset of the columns of tables A and B have similar data and therefore could make a union without a mismatch of the number of columns or types.

## Intersection 

Intersection keyword is where we will use table A and table B, and find a set of where they are both common.

```sql
SELECT firstname, lastname, address FROM customers
INTERSECT
SELECT firstname, lastname, address FROM employees;
```

* We want to find all customers who are also employees
* We want to find all students who are also staff members


## Difference/Except

This operator use to not exist within MariaDB/MySQL until roughly version 10. However there were some oddities with its implementation.

The `EXCEPT` keyword is where we will use table A and table B, and retrieve results where we find customers who are also not employees.

```sql
(SELECT firstname, lastname, address FROM customers)
EXCEPT
(SELECT firstname, lastname, address FROM employees);
```

* We want to find all customers who aren't employees
* We want to find all students who aren't staff members

Do note, from my own experience the syntax with EXCEPT is a little funny, I have come to use paranthesis around my queries when performing set operations but occasionally MySQL workbench will interpret it correctly but other DB clients will.

## Notes on Cartesian Products

*Hang on! What about that Cartesian Product issue?*

Oh yeah! Actually, all our joins in theory can be a cartesian product, however our queries get opimised by the database engine.

You typically wan tot avoid any query that can produce a cartesian product as this has a huge space and time cost associated (A lot of memory needed and a lot of processing will need to be done).

