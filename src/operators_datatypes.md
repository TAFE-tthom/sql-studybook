# Common Operators and Data Types

As outlined previously, Data types within SQL have **operators** that are used on **operands**. However, there is a relationship between **operand** and **operator** where depending on the **operand** type, the **operator** may perform a different action.

We have observed some basic operators in use. The most common kind of operator you will encounter are **binary operators**. However, there is another common kind of operator you will use called an **unary operators**.

Common operators within SQL will be grouped like so.

**Arithmetic Operators**

The following operators relate to common programming functionality. That being

* `+` - Addition
* `-` - Subtraction
* `/` - Division
* `%` - Modulus
* `*` - Multiplication


**Logical Operators**

Logical operators are used when we want to evaluate if something is true or false. THis is useful for when your query needs to makes decisions.

* `<` and `<=` which corresponds to less than and less than or equal to.
* `>` and `>=` which corresponds to greater than and greater than or equal to.
* `=` which correspond to an **equality** check. However this operator is also used as part of assignment,
* `&&` and `AND` which correspond to logical AND, which means both LEFT and RIGHT operands have to result in being true. Alternatively, `||` and `OR` corresponds to logical OR, which means only one of the operands has to be true for the expression to be true.


