# Exercises

### 1. Action Films

Construct a view that will return a list of films that correspond to the action category.


### 2. Cities and Countries

Using the sakila database, construct a view that will represents an inner-join
between city and country. The view should only return the city and country names but have an inner join behind them.



### 3. Films that are not rented out

Using the sakila database, construct a view that will discover what films have not been rented out. You will need to use the `current_date` (or a specified date for testing).

### 1. Promotion Send Out

Firstly, you will need to create a table called `promotions` that will have the columns `customer_id`, `promotion_date`, `discount_code`. 

Create a trigger on the `rentals` table that will note down a promotion that was sent out to the customer after they have rented out a film.

