# Aggregate Queries, Structure and Functions

When working with SQL, we may need to operate on a collection entries rather than a particular entry. 


## `GROUP BY`

We have briefly seen `GROUP BY` being used when we have performed a table selected in some of the examples linked. `GROUP BY` is used where we need to associate a particular entry with an aggregate.

There are a number of built-in functions that allow the database developer to operation on not just a single portion of data but over a collection or set.

The following functions can be used as aggregate functions. However we need to be mindful in how we group it with a field or if we use it on the whole table.

* `COUNT`
* `MIN`
* `MAX`
* `SUM`

Lets look into how we can use `GROUP BY` with `SUM`.

```sql
SELECT SUM(amt), Destination FROM
Orders
GROUP BY Destination;
```

The above query breaks down where the `SUM()` aggregate function is going to be associated with the column `Destination`.

The output of the following will be:

```
|SUM(amt)|Destination|
+--------+-----------|
| 350.50 | Sydney    |
| 401.24 | Melbourne |
| 122.23 | Hobart    |
```

We can observe that the `SUM(amt)` column reflect the summation of all times `Destination` and `amt` are referenced and where `Destination` matches something seen or is first encountered.

So, what happens is prior to the output, we may have two entries like so:

```
| 125.00 | Sydney |
| 225.50 | Sydney |
```

Merges to:

```
| 350.50 | Sydney |
```


Since we are intended to sum the `amt` column and we see the `Group By` column referenced as `Sydney`. We will then add `125.00` and `225.50` together and associate it with `Sydney`.

## Applying predicates with `HAVING`

The `Having` keyword within `SQL` is similar to the `WHERE` keyword. However, it is targeted for specifically for aggregates.

So, within the statement prior, we are able to add an additional clause for looking for amounts above `200`.

```sql
SELECT SUM(amt), Destination FROM
Orders
GROUP BY Destination
HAVING SUM(amt) > 200.0;
```


By now limiting it to > 200.0, we are able to apply a constraint on the aggregate.

```
|SUM(amt)|Destination|
+--------+-----------|
| 350.50 | Sydney    |
| 401.24 | Melbourne |
```

**Why `HAVING` and not `WHERE`?**

The answer here is that we are to be specific to aggregates, `HAVING` is to apply the constraint on a *potential* result. The `WHERE` is to be applied directly onto entry within the table itself.

