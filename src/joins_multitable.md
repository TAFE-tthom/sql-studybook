# Using Multiple Tables and Cartesian Products

We have been currently working with just a single table (except for people who have finished the last two exercises with their homework). 

A simple way we could just use multiple tables is by just appending another table after the `FROM` keyword.

```sql
SELECT * FROM Customers, Employees;
```

You will observe that there is a lot of data that has bene produced. In-fact! It has actually exceeded the sum total of records in both `Customers` and `Employees`.

So we need to ask, how this could be? We need to then examine what a **Cartesian Product** is.

## Cartesian Product

The operation we have performed here is that we have created a result in which for every entry in table A, we have an entry that is combined with Table B. This is known as a cartesian product. This is a term you may have heard from school.

Where we have X, Y coordinates where (1, 1) is a point in space, these are referred as cartesian points.

*Do note! As a mathematical construct, SQL Tables are Sets and numbers that represent a particular domain like Integers and Decimals are also Sets*

* If this is your intention, you typically want to specify `CROSS JOIN` between the two tables.


### Why we should avoid them

Usually we aren't after both tables being smashed together and this results in **A LOT OF DATA** being generated and held in memory, especially if we are looking for a particular element.

However it is possible that the query may naturally be required to perform this kind of construction as we could be looking at building all permutations.
