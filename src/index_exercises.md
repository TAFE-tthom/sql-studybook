# Exercises

## Tasks

### 1. Key Candidates 1

Note: You do not need to write SQL for this answer

You have been given a client brief to implement part of a database system for
a post-office network.

The segment of the network  you are working on is composed of:
* Sorting Centres
* Post Offices

A sorting centre will handle:
* Parcels
* Mail

Each sorting centre has an address and post offices that it services

Post offices will parcels and mail it is holding and from what sorting centre they have come from as well as a manager in-charge.

There are two parts to this question:

1. What tables would you construct, outline the columns you can directly
derive and ones you have inferred. Outline what columns are primary keys, foreign keys and unique indexes.

2. Given that the amount of information is not comprehensive enough to
build a full system or even a part of the system, do the following:

* Outline 2-3 questions you would ask to clarify how you would design the
database

* Outline your assumptions you have made when outlining the tables and columns in part 1.

### 2. Apply your constraints

You have been the table below to identify what columns would be
good candidates for a primary key and unique index.

```sql
CREATE TABLE Customer (
  customer_id INT NOT NULL,
  name VARCHAR(512) NOT NULL,
  email VARCHAR(512) NOT NULL,
  street VARCHAR(1024) NOT NULL,
  city VARCHAR(256) NOT NULL,
  country_code CHAR(4) NOT NULL,
  age INT NOT NULL,
);
```

Alternative the table above and provide a rationale behind your
changes.


### 3. Checking post-offce rules

Let's look at an extension from question 1.

Your database will now need to handle a constraint where a post-office
could only allow a certain amount of parcels being delivered to it.

There are different post-office sizes and their capacity can be determined by that size.

* Village (100-499 parcels)
* Town (500-20000 parcels)
* City (30000-50000 parcels)

The number of parcels it could support is separate from the kind of post-office size but that it should be within the constraints of the size.

If a post office is serving a village, its capacity could range between 100-499.


1. What new column(s) would you introduce to the tables you have outlined in question 1.

2. You will need to build some relationship between Parcels or PostOffices, consider and action the following.

* What tables would you introduce to link Parcels and PostOffices (Consider a joining table).

* How would you integrate a way to check the constraints are enforced. Consider where/how you would use `CHECK` and if you would make it a relational constraint.
