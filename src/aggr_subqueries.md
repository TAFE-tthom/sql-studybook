# Subqueries

We will be looking into subqueries. Subqueries themselves are inner queries within a select statement.

These can occur within a column or as part of a FROM statement or in a where clause. These have a purpose of utilising tables that you will need to complete as part of another query.

Lets look into an example of a subquery.

```sql
SELECT *
FROM [OrderDetails]
WHERE [OrderDetails].[OrderID] = (SELECT TOP 1 [Orders].[OrderID]
	FROM [Orders] ORDER BY [Orders].[OrderDate] DESC)

```

The above query is retrieving all elements from the Orders tables where the OrderID matches the first OrderID in Orders.


## Evaluation and Correlated Subqueries

It is necessary to discuss how evaluation works with subqueries, in particular with **correlated subqueries**.

```sql
SELECT *
FROM [OrderDetails]
WHERE [OrderDetails].[OrderID] = (SELECT TOP 1 [Orders].[OrderID]
	FROM [Orders] ORDER BY [Orders].[OrderDate] DESC)

```

Naively, the inner query is usually executed and evaluated first, however an optimisation can be applied to retrieve a value or for the database engine to speculate what the engine could be.

What is important though is to acknowledge that since the `WHERE` clause is dependent on the result from another query, the outer query cannot get executed in-order.

### Correlated/Nested Subquery

A correalted subquery that is mostly effective and efficient is where the subquery can be relegated to each tuple. This is based on granularity of the subquery.

```sql
SELECT
  Orders.order_id AS OrderID,
  (
    SELECT SUM(amount) FROM OrderDetails
    WHERE OrderDetails.order_id = OrderID
  )
  AS AmountTotal,
  (
    SELECT SUM(paid) FROM OrderDetails
    WHERE OrderDetails.order_id = OrderID
  )
  AS AmountPaid
  FROM Orders 
```

We can observe two subqueries within the above query. However the subqueries are not beholden to the result of another tuple, we are able to get the `OrderID` and execute the subquery.

However this is still a correlated query as the outer and inner queries are still reference, however there are a number of optimisation paths that can be formed.

* Caching the results from the SUM
* Reducing the SUM on `OrderDetails`
* `order_id` and `OrderID` being keys will reduce the search time


