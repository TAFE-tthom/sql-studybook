# Views and Cache

A view is a virtual table, it is similar to a table but it maps to an existing table is a select operation.


## Views

These virtual tables are a subset of a table/query which are designed to be queried themselves. Given a view can be queried.

A very simple query could look like this
```sql
SELECT * FROM viewCustomers;
```

Lets go through the following.

```sql
CREATE VIEW vw_outstanding_rental_report
AS
SELECT rental.rental_id, rental.rental_date, rental.return_date,
	film.title, film.[description]
FROM rental
INNER JOIN inventory
ON rental.inventory_id = inventory.inventory_id
INNER JOIN film
ON inventory.film_id = film.film_id
WHERE rental.return_date IS NULL;
```

We start by creating a view and providing an identifier.

We then start a sql query by using a `CREATE VIEW` keyword phrase. We then provide an identifier of the view name. It will then be followed by the body of the view which is just a query.

### Why use views?

While it can be confusing, they have a few different purposes over simply submitting queries every time. Views are a mechanism which serve the following purposes.

* Caching results from querying it

Since the SQL associated with the view has been evaluated and computed, it can cache the results from the query within it.

* Nominally, read-only

Complex queries within a view cannot have an insert applied on them. Only if the view essentialy reflects a single table it is referring to.

* Abstraction

Without needing to create a whole new table and duplicate data or keys, a view becomes a virtual table in which can be an elegant combination of many tables or joining tables.
