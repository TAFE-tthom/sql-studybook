# Inner Join, Left Join, Full Joins

We will be covering on a number of joins within this segment. You will find that there is a link between **Cartesian Products** and joins, especially with full joins.

## Inner Join

With an inner join, we are usually searching for the **intersection** of both tables. Typically where one table has a matching identifier on the other.

These are common, where we say like:

* We want to find all times an employee started and finished
* We want to find all albums that match a genre

Lets focus on the following.

```sql
SELECT
  Employees.First_Name,
  Employees.Last_Name,
  Hours.Clock_In,
  Hours.Clock_Out
FROM Employees
INNER JOIN Hours ON Employees.ID = Hours.ID
WHERE Employees.First_Name = 'Helmholtz';
```

The query is performing a join on Employees and Hours, and matching the Employees ID to the Hours ID column. These are to match up records from table Employees to any record in table Hours if it has the same ID.


## Left Join

Left Join and also **Right Join**, what is included is all elements in the *left* table even if matches.

Lets focus on the following.

```sql
SELECT 
  Customers.Company,
  Customers.[FirstName] + ' ' + Customers.[LastName],
  Orders.*
FROM Customers
LEFT JOIN Orders
ON Customers.ID = Orders.[CustomerID];
```

To reiterate and relate to the query above.

The above query selects all from customers and matches on orders where an order has a customer id that matches. It will also include all customers regardless if a customer has made an order.


## Full Outer Join

`FULL JOIN` or more specifically `FULL OUTER JOIN` can seem very similar to a `CROSS JOIN`/cartesian product. However it is doing something subtle with the results it returns when it does not match.

Lets create a variation on the previous query.

```sql
SELECT 
  Customers.Company,
  Customers.[FirstName] + ' ' + Customers.[LastName],
  Orders.*
FROM Customers
FULL OUTER JOIN Orders
ON Customers.ID = Orders.[CustomerID];
```

The above query selects all from customers and matches on orders where an order has a customer id that matches. **It will include all customers and orders**.

*Wait... this seems like a catesian product?*

The main observation here is that `CROSS JOIN` or Cartesian Products are not performing a match while a full outer join is at least doing some form of matching.

The main key here is substitution and combination. If it includes results from all, does it necessarily combine?

You will observe that without a match an entry will likely contain nulls or a default value.





