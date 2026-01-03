# Indexes and Unique Columns

We have constructed tables with primary keys. The role that primary keys take are an index in which we are easily able to retrieve an element.

However, if we need to have faster searches, we should also be able to search other columns other than the primary key. However, Foreign keys also are indexes, however they are a little quirky. 

## Indexing

Since we know that when data is indexed, we can usually consider that the data is unique to a row, knowing this, means we aren't going to have to sift through duplicates, we can simply use the id and immediately go to the location required.

### Linear Searching

Firstly, lets understand what happens when we don't have an index/primary key on a table.

Lets consider what will happen when we take the following query into code.

```sql
SELECT name FROM employees WHERE employee_id = 788;
```

Since `employee_id` is not a primary key, the query will translate into something like this.

```js
let employee_id = 788;
for(let i = 0; i < employees.length; i++) {
  if(employee_id === employees[i].employee_id) { return [ employees[i].name ]; }
}
return [];
```

### Uniqueness and Ordering is useful

An alternative to indexing efficiently is to use a unique index on a column. This will be associated with the table object.

Unique index serve a similar purpose to a primary key. 

### Indexing and Sublinear Searching

We just need to find one element within the table when searching for a unique id. So, we can
avoid looking at elements that aren't of interest to us if we know what would be suitable.

```sql
SELECT name FROM employees WHERE employee_id = 788;
```

Since employees now has a primary key on employee_id, we can also assume that the data is in order. By doing this, a different algorithm can be employed such as a binary search.

```js
let employee_id = 788;
let left = 0;
let right = employees.length - 1;
let match = [];

while(left <= right) {
  let mid = Math.ceil((left + right) / 2);
  if(employees[mid].employee_id === employee_id) {
    match = [ employees[mid].name ]; break;
  } else if(employees[mid].employee_id < employee_id) {
    left = mid;
  } else {
    right = mid - 1;
  }
}
return match;
```


## Foreign Keys are Indexes

When a foreign key is established, we are able to use the key from another table and apply it the table which holds the primary key (which is intuitive and already established).

However, when a foreign key is formed, it will be applied along with a group of records that are associated with a foreign key value. Since the foreign key can appear multiple times within a table, the reduction associated with the search time is on finding the group, not necessarily the individual record.


## Metadata

We have seen how primary keys play out but what about unique indexes?

It isn't as simple to order data when we have two distinct orderings. The solution
is to maintain additional data structure that maintains a different ordering.

This is a form of meta-data within the database and is dependent on the optimisation
the database engine wants to employ.

## Unique Constraints

A unique constraint when assigned to a table enforces a rules to ensure that all tuples
within the table have a unique value for that column.

This is useful to apply for certain kinds of data where we want to mitigate duplicate
entries 

We can look at the following example where we have a unique constraint applied to email.
Since a customer would have a unique email, we would ensure that we constrain any new customer to
only have a unique email.

```sql
CREATE TABLE Customer (
  customer_id INT NOT NULL,
  email VARCHAR(512) NOT NULL,
  name VARCHAR(512) NOT NULL,
  age INT NOT NULL,
  UNIQUE(email)  
);
```


