[Index](index.html)  [Home](getting-started_home.html)

Hint

`Hint` is a clause in a [For](4gl_for.html) instruction that accesses the database and instructs the database system the best strategy to follow to get the required data.

# Syntax

```
For [abv]key1 Hint Key key2
For [abv]key1 Hint Key =expression
For [abv]key1 Hint Key key2 Where condition 
For [abv]key1 With Nohint
For [abv]key1 Where condition With Nohint
```

# Examples

```
# Access to customer data (table BPCUSTOMER with two keys : BPC0 (BPCNUM column), BPC1 (BPCNAM column).

# This hint is useless because using the BPC1 key is obvious if the condition is placed on the key value
Local File CUSTOMERS [BPC]
For [BPC]BPC0 Hint Key BPC1 Where pat(BPCNAM,"J*")<>0
 ...
Next

# Here we give the rank of the key to be used and keynam gives back the name of the key in the formula
Local Integer KEYNUM=1
For [BPC]BPC0 Hint Key =[G:BPC]keynam(KEYNUM) Where pat(BPCNAM,"J*")<>0
 ...
Next

# Let's make the database to define the strategy to get the customer records in BPC0 order (default rule)
For [BPC]BPC0 Where pat(BPCNAM,"J*")<>0 With Nohint
 ...
Next

# Let's make the database to define the strategy to get the customer records without giving an order (default rule)
For [BPC]reckey Where pat(BPCNAM,"J*")<>0 With Nohint
 ...
Next
```

# Comments

This type of syntax should be reserved for exceptional cases, for the following reasons:

* The use of a `Hint` can have a positive effect on a database, and a negative one on another database. This makes the optimization database dependent.
* In most of the cases, the database engine is able to optimize the access strategy dynamically depending on statistics calculated regularly. This kind of hint creates a static optimization.
* Even if a `Hint` can improve performance, do not forget that every new database version can enhance the situation and make the `Hint` clause useless or even harmful in term of performance.

# See also

[File](4gl_file.html), [For](4gl_for.html), [Filter](4gl_filter.html).

  

[Index](index.html)  [Home](getting-started_home.html)