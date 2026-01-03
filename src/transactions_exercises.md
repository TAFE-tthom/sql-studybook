# Exercises

## Tasks - Stored Procedures and Functions

### 1. Inserting customers

Create a stored procedure called `sp_NewCustomer`, this procedure will be responsible
for creating a new customer in the `customer` table.


### 2. Most prominant actor

You need to create a stored procedure called `sp_ProminantActor`, the function will accept a `film_id` and work out the most popular actor in the list. Consider using a subquery to solve this.

### 3. Get the manager

You need to create a stored procedure called `sp_GetManagerFromRental` that will have a `rental_id` as a parameter. Given a `rental_id`, we should be able to trace the store and manager responsible. The manager name should be return by the function.


### 4. Format Customer

Create a function that will format customer data, the function will be called:
`fn_FormatCustomer` which will have the following parameters:
  * `customer_id`: INT
  * `first_name`: VARCHAR
  * `last_name`: VARCHAR

The function itself will format the output so the output will look like:

```
CustomerNo: <customer_id>
First Name: <first_name>
Last Name : <last_name>
```
Example:

```
CustomerNo: 29
First Name: ANGELA
Last Name : HERNANDEZ
```


It will be used in the following query:

```
SELECT fn_FormatCustomer(customer_id, first_name, last_name)
  FROM customers
  WHERE customer_id = 10;
```



### 5. In Date Range

Create a function that will be used to check and filter rentals. The function will be called `fn_RentalsInDateRange`, it has three parameters and returns a boolean value (true or false).
  * `start_date`: DateTime
  * `return_date`: DateTime - `return_date` of a rental is inputted here 
  * `end_date` : DateTime

The function will be used in the following query:

```
SELECT * FROM rentals
  WHERE fn_RentalsInDateRange('2005-05-24 00:00:00',
    return_date,
    '2005-05-27 00:00:00')
```


