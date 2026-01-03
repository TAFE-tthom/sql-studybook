# Transactions

Transactions are an important concept within databases but also within programming as well. Primarily the focus or problem it is handling is relation to concurrency. This involves multiple operations being processed concurrently (or in parallel).

In part the complexity is the ordering of a transaction and ordering of one.


## ACID

1. Atomicity

We consider a transaction as a single unit of work. Atomicity is to ensure that the individual operations related to the transaction must all be completed or fail.

This is to prevent partially completed work.


2. Consistency

Consistency is to ensure that the database is able to be returned or not be in a state which is incosistent with itself or other networked databases. (Database synchronisation and shards).

3. Isolation

When transactions are executed, they should be isolated from the effects from other transactions. This is because if another transaction writing/reading occurs, the order in which data is available is not going to be consistent.

Therefore we want to ensure that order is reprsented in serialized form.

4. Durability

Realistically, durabiity is to mean that once it is comitted, in the event of a power-outage/system failure, the data will remain, partially written data will not be committed.

## Grouping Operations

Insertions on their own are a transaction by default, this results in where any record will result in an individual transaction per record.

So, when we are explicit and turn off the autocommit of transactions, we arrange a block of our transactions, we specify that we don't want it to bean automatically commit. 

So what does a transaction look like?

```sql
SET AUTOCOMMIT = OFF;
START TRANSACTION

--- statements

COMMIT;
```
All statements within the `START TRANSACTION` and `COMMIT` block.

By itself this seems arbitrary but what is interesting with transactions is that they are meant to prevent issues where there is an overlap between transactions/operations.

### Errors, Rollbacks and Commits

When known that a transaction will fail, you will need to create a handler for `SQLEXCEPTION` in which it is able to update a `boolean` variable when the exception is triggered.

Use following segment when want to detect an exception has occurred.

```sql
DECLARE rberr BOOL DEFAULT 0;
DECLARE CONTINUE HANDLER FOR SQLEXCEPTION SET rberr = 1;
```

Afterwards, the following is leveraged to indicate if an operation prior had failed and should therefore rollback or if it should commit.

```sql
-- ... snippet above

-- INSERT statement which could fail

IF rberr THEN
  -- Your segment here
  ROLLBACK
ELSE
  -- Either not needed
  COMMIT
END
```

A rollback is when there is an issue with a transaction outside of a general error within the transaction block, you are able to trigger `ROLLBACK`.


### Further Reading


When optimising and utilising hardware capabilities, we are able to leverage multiple cores. However by doing this we can run into issues where 'lose data' after an update.

Fortunately, Majority of the SQL implementations treat each query as their own transactions.

For further information you will need to look into the following topics:

* Serializability
* Linearizability
* Transactional Memory
