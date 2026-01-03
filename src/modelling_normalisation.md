# Database Normalisation

We sometimes don't get much of a chance to design databases from scratch.

So we may need to undertake "refactoring" but this could be even refactoring during developing.

Normalisation is a process of untangling and refactoring the database design by moving it to a **higher form**.

A **form** within this area is a category that the database and tables much exhibit.

Common **forms** that databases typically satisfy.

* 1NF
* 2NF
* 3NF
* BCNF
* 4NF


## Starting with unormalised data

For some context here, this kind of data could have come from a device that generates, spreadsheet from a business or how the data was merged.

We also need to acknowledge that we have to have some domain knowledge as well.

```
| Artist         | Album     | Format               | Genre      | Price        |
|----------------|-----------|----------------------|------------|--------------|
| Maribou State  | Portraits | [Vinyl, CD, Digital] | Electronic | [49, 20, 10] |
```

### 1NF

To satisfy 1NF.

Each field contains a single value and must not contain nested records.

We are looking for records that may be multi-valued. So, lets look at the data from before.

```
| Artist         | Album     | Format               | Genre      | Price        |
|----------------|-----------|----------------------|------------|--------------|
| Maribou State  | Portraits | [Vinyl, CD, Digital] | Electronic | [49, 20, 10] |
```

We can identify that Format is an aggregate that is used within it.

```
| Artist        | Album     | Format  | Genre      | Price |
|---------------|-----------|---------|------------|-------|
| Maribou State | Portraits | Vinyl   | Electronic | 49    |
| Maribou State | Portraits | Digital | Electronic | 20    |
| Maribou State | Portraits | CD      | Electronic | 10    |
```

We do have another problem though, we now have repeated entries with the exception of the `Format` and `Price` columns.

### 2NF

To satisfy 2NF.

If a subset of the key is a determinant. As in we have a column in which determines the differences between the records, this concludes that when we have a composite key, the composite key is using a field that could be reduced or moved to a separate table.

Using the previous 1NF adjustment, we now get to address the next part.

```
| Artist        | Album     | Format  | Genre      | Price |
|---------------|-----------|---------|------------|-------|
| Maribou State | Portraits | Vinyl   | Electronic | 49    |
| Maribou State | Portraits | Digital | Electronic | 20    |
| Maribou State | Portraits | CD      | Electronic | 10    |
```

We can identify that once again `Format` and `Price` are associated with `Artist` and
`Album`. 

We will use Album, Format and Price and specify it in another table but we will modify the original table to only have Artist and Album.

Albums:
```
| Artist        | Album     | Genre |
|---------------|-----------|-------|
| Maribou State | Portraits | Elec. |
```

AlbumFormats:
```
| Artist        | Album     | Format  | Price |
|---------------|-----------|---------|-------|
| Maribou State | Portraits | Vinyl   | 49    |
| Maribou State | Portraits | Digital | 20    |
| Maribou State | Portraits | CD      | 10    |
```

### 3NF

To satisfy 3NF.

We are looking for a transitive functional dependency.

In the case for a transitive functional depdenency. This is where the domain information can be handy but also identifying where within a table, a column is dependent on another column.

A clear example would be Author having Author Nationality, the Nationality is dependent on the Author and is updatable.

Albums:
```
| Artist        | Album     | Genre |
|---------------|-----------|-------|
| Maribou State | Portraits |  1    |
```

AlbumFormats:
```
| Artist        | Album     | Format  | Price |
|---------------|-----------|---------|-------|
| Maribou State | Portraits | Vinyl   | 49    |
| Maribou State | Portraits | Digital | 20    |
| Maribou State | Portraits | CD      | 10    |
```

Genres:
```
| GID | Genre |
|-----|-------|
| 1   | Elec. |
  
```

*Wait! What is the trick here? How are you coming up with the new design?*

For the most part, we are attempting to resolve the violation that has occurred. Aftwards, we are then attempting re-design it then satisfy it.

We can also decompose the structure further to also make `Format` itself a table.


### BCNF

Functional dependency, it should either be a super key or the cadidate key. As in, if a column (B) is dependent on another (A) and A is a candidate key. Otherwise there is a violation.


Classes:
```
| SID | Class    | InstructorID |
|-----|----------|--------------|
| 1   | Painting | 1            |
| 2   | Painting | 2            |
| 2   | Software | 3            |
```
We can break this apart and utilise a primary id for the entry. This is moving towards out joining tables.

StudentClasses:
```
| SID | Class    |
|-----|----------|
| 1   | Painting |
| 2   | Painting |
| 2   | Software |
```

---

InstructorClasses:
```
| ID  | Class    |
|-----|----------|
| 1   | Painting |
| 2   | Painting |
| 3   | Software |
```

### 4NF

What is interesting with 4NF is that is mostly along the a similar set of rules as BCNF however it more strictly enforces that if there is a compound candidate key, it will indicate utilising a primary key that is part of the sequence. 

Given the prior BCNF, we actually would break the Class to be a primary key and moved to its own table.

Classes:
```
| CID | Class    |
|-----|----------|
| 1   | Painting |
| 2   | Software |
```

---

InstructorClasses:
```
| ID  | CID |
|-----|-----|
| 1   | 1   |
| 2   | 1   |
| 3   | 2   |
```

## Summary

* Representation of databases can be encapsulated in a Crow's Foot notation and Chen's Notation.

* Develop database models from early conception to their physical implementation.

* We can handle data and structure that may contain repetition and also enforce relational rules.

