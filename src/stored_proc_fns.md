# Stored Procedures and Functions

Procedures are typicalled design and focused with performing an action. They will similar to builtin functions that we have used before but their execution/call is different.

## Stored Procedure Example

Let's break down and construct a stored procedure for `Sakila` database.
 
* `citycount` is an identifier of the procedure.
* `country` is an input parameter
* `cities` is an output paramter

Procedures do not return a result. The use-case for procedures is usually for performing updates or insertions.

```sql
CREATE PROCEDURE citycount (IN country CHAR(3), OUT cities INT)
       BEGIN
         SELECT COUNT(*) INTO cities FROM world.city
         WHERE CountryCode = country;
       END
```

The above stored procedure simply returns the count and is assigned to cities parameter. We have the parameter country which is a 3 letter country code used as part of the query.

Do note, when constructing a stored procedure within **mysql** will require changing the `DELIMITER` from `;` to something else (commonly `$$`). This is to avoid confusion or issues with the parser when constructing it.

### Stored Procedure and Transactions

We are able to mix transactions elegantly with stored procedures and these end up being a reasonable location to use them.

We will use the following segment and decompose it.

```sql
SET autocommit = 0;
DELIMITER $$

-- Revisit this to parameterise it
CREATE PROCEDURE SP_AddStaffMember()
BEGIN

 DECLARE rberr BOOL DEFAULT 0;
 DECLARE CONTINUE HANDLER FOR SQLEXCEPTION SET rberr = 1;

 START TRANSACTION;
 -- Get the country id
 SET @countryid = (SELECT country_id FROM country WHERE country = 'Australia');

 -- Get the city id and also insert the city
 SET @cityid = (SELECT city_id FROM city WHERE city = 'Brisbane');

 -- Insert the new address
 INSERT INTO address(address, district, city_id, postal_code, phone) 
  VALUES ('98 Martin St', '', @cityid, '6000', '');
 -- Get the address id
 SET @addressid = (SELECT address_id FROM address ORDER BY address_id DESC LIMIT 1);

 INSERT INTO staff(first_name, last_name, address_id, 
  picture, email, store_id,  active, username, password)
  VALUES('Martin', 'Forest', @addressid, 
  NULL, 'martin.forest@sakilastaff.com', 2, 1, 
  'martin', 'e38ad214943daad1d64c102faec29de4afe9da3d');
 IF rberr THEN
  SELECT 'Rolling back, error detected';
  ROLLBACK;
 ELSE
  SELECT 'Committed, no error found';
  COMMIT;
 END IF;
END$$

DELIMITER ;

CALL SP_AddStaffMember();

```

1. We have set the autocommit to 0, which means all reads and writes are going to be considered a single operation, if one fails they should all fail.

2. We have created a procuedre which will add a staff member

3. We have created an SQL handler and will use that towards the end of the stored procedure.

4. We have retrieved the countryid and city of `Australia` and `Brisbane`. However it is usually common to insert new information if it is not present in the database.

5. We have inserted a new address into the address table and retrieved the address id.

6. Finally the transaction will insert the staff member and use the address id variable inside it. This could still fail if the address itself was not able to be inserted or if the staff couldn't be.

7. If an error occurs, it will rollback, otherwise it will commit.

We can modify the stored procedure to have parameters instead of using the default values there.


## Functions

Similar to other programming languages, we are capable of creating our own functions within SQL. These follow a similar syntax to stored procedures. However, they are able to called inside query readily.

```sql
CREATE FUNCTION hello_world(msg VARCHAR(100)) RETURNS STRING
RETURN (SELECT msg);
```

The above function is broken up into 3 different components.

Parameters, Return type and Body (which includes a return that provides the data).

We are able to create our own functions and specify our own parameters.
There are a few different parameter qualifiers to be awarey about.

* `IN` which specifies the paramter is input only
* `OUT` which specifies the parameter is an output variable and will
  change the value post-function call. Typically only designed
  for mutation
* `INOUT` which specifies the parameter is both mutation and reading.

```sql
CREATE FUNCTION addthree(IN x INT, IN y INT, IN z INT) RETURNS INT
BEGIN
  RETURN x + y + z;
END;
```
