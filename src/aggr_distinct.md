# Distinct and In

## Distinct

The distinct keyword is used to reduce what would normally output a duplicate records. If a column/combination of column contains a duplicate, it will only output only one match instead of multiple.

```sql
SELECT DISTINCT City FROM Customers; 
```

You want to find out what cities that all customers are from. The above query will achieve this.


## `IN`

The `In` keyword is used to utilise the returned records and detect if an element exists in them.

```sql
SELECT * FROM Customers
WHERE Country IN ('Singapore', 'New Zealand', 'Australia');
```

This will retrieve all customers that are from Singamore, New Zealand or Australia.

```sql
SELECT * FROM Customers
WHERE Country IN (SELECT DISTINCT Country From Customers LIMIT 3);
```

The above query will retrieve the first 3 countries from the customer list
and retrieve all customers that are from those countries.
