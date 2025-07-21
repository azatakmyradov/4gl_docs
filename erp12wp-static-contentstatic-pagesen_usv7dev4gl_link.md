[Index](index.html)  [Home](getting-started_home.html)

Link

`Link` is used to define joins between database tables to access, with single abbreviation, these tables with one [Read](4gl_read.html) or [For](4gl_for.html) instruction.

# Syntax

```
 Link [MAINCLASS] With LINK_LIST As [LINKCLASS]
 Link [MAINCLASS] With LINK_LIST As [LINKCLASS] Where WHERE_CONDITIONS
 Link [MAINCLASS] With LINK_LIST As [LINKCLASS] Order By ORDER_EXPRESSIONS
 Link [MAINCLASS] With LINK_LIST As [LINKCLASS] Where WHERE_CONDITIONS Order By ORDER_EXPRESSIONS
```

* `MAINCLASS` identifies the main table from where the joins are done. It is the table that has the lowest level of details. The table must have been declared previously.
* `LINK_LIST` is a list of `LINK_CONDITION`s separated by commas. At least one, and at most 11 `LINK_CONDITION`s can be given. Up to 12 tables can be together in a `Link`syntax.
* `LINKCLASS` is the abbreviation to the join. A [Read](4gl_read.html) or a [For](4gl_for.html) on this abbreviation will perform the join and get the data.
* `WHERE_CONDITION` is a filtering condition. For more information, see the [Where](4gl_where.html) documentation.
* `ORDER_EXPRESSION` is an ordering clause. For more information, see the [Order By](4gl_order-by.html) documentation.
* `LINK_CONDITION` has the following syntax:

```
  [CLASS]KEY_NAME = EXPRESSION_LIST
  [CLASS]KEY_NAME(INDEX_VALUE) = EXPRESSION_LIST
  [CLASS]KEY_NAME ~= EXPRESSION_LIST
  [CLASS]KEY_NAME(INDEX_VALUE) ~= EXPRESSION_LIST
```

* `CLASS` is the abbreviation of the table in which a join is done. This table must already have been opened.
* `KEY_NAME` is a key of this table.
* `INDEX_VALUE` is an integer expression that returns the number of components used to define the join.
* `EXPRESSION_LIST` is a list of `EXPRESSION`s separated by semicolons.
* `EXPRESSION` is an expression that might include constants, variable available in the context that will be evaluated and considered as constants, and columns of the main table or other tables that have already been joined in the join list.

With the syntax using `=`, the join done is a left outer join. With the syntax using `~=`, the join done is an inner join (which is preferable, from a performance point of view, when possible):  
\* a left outer join means that if a line has no valid joined line, the main line will appear nevertheless  
\* an inner join will select only the lines that have a valid join.

# Examples

```
   # First simple example
   # Access to X3 customer table and to information related to the creation user (that still exists)
   Local File BPCUSTOMER [BPC], AUTILIS [AUS]
   Link [BPC] With [AUS]CODUSR~=[BPC]CREUSR As [BPUSR]

   # Second example
    Access to X3 customer, to creation user information and to modification user (when it exists)
   Local File BPCUSTOMER [BPC], AUTILIS [AUS], AUTILIS [AUS2]
   Link [BPC] With [AUS]CODUSR~=[BPC]CREUSR, [AUS2]CODUSR=[BPC]UPDUSR As [BPUSR2]

   # Third example (not based on standard Sage X3 tables) 
   # Let's imagine we have a sales history table called HISTORY [HIS]
   # In this table, we store the key of the customer HISCUST, the key of the product HISPROD
   # and the key of a salesrep HISREP (not always filled)
   # The other tables we want to perform a join with are:
   # CUSTOMER [CUST] table: a main key CUSKEY (1 component CUSTCODE). It includes a COUNTRY code (COUNTRY)
   # PRODUCT [PROD] table: a main key PROKEY (1 component PROCODE)
   # SALESREP [SREP] table: a main key PROKEY (1 component PROCODE)
   # PRODDES [PRDE] table: product description per language. The key PRODES has 2 components (PRO,LANG)
   # The product descriptions are not necessarily available for all the languages
   # COUNTRY [COUN] table: a main key COUNKEY (1 component COUNCODE). Includes a language code (LANCODE).
   # CONDITION is a string that has been transmitted by a calling script. Every column of one of the joined
   # tables can possibly be present there
   Local File HISTORY [HIST], CUSTOMER [CUST], PRODUCT [PROD], SALESREP [SREP], COUNTRY [COUN], PRODDES [PRDE]
  # The link is here a unique instruction (this is why we have an '&' at the beginning of the next lines)
  # The order in which the join condition are given is important:
  # The join on [COUN] cannot be done before the join on [CUST] because it requires a column from [CUST]
  # The join on [PRDE] requires a column from [COUN] and can therefore not be done before [COUN] and [CUST]
   Link [HIS] With
&  [CUST]CUSKEY  ~= [HIST]HISTCUST,
&  [PROD]PROKEY  ~= [HIST]HISTPROD,
&  [SREP]REPKEY   = [HIST]HISTREP,
&  [COUN]COUNKEY ~= [CUST]COUNTRY,
&  [PRDE]PRODES   = [HIST]HISTPROD; [COUN]LANCODE
&  As [HISLNK]
&  Where evalue(CONDITION)
&  Order By Key KEYHIST=[HIST]HISTDATE;[CUST]CATEGORY;[HIST]CUSKEY;[PROD]PROKEY
  # Now we can use it
    For [HISLNK]KEYHIS(1) Where [CUST]COUNTRY="USA" and [PROD]CATEG=1: # Combines with CONDITION
      # In this loop, we have [HIST], [CUST], [SREP], [COUN], [PRDE] on line
      # A loop is performed for every distinct HISTDATE
      For [HISLNK]KEYHIS(2)
        # A loop is performed for a given HISTDATE, for every distinct customer CATEGORY
        For [HISLNK]KEYHIS(3)
          # A loop is performed for a given HISTDATE and customer CATEGORY, for every distinct CUSKEY
          For [HISLNK]KEYHIS(4)
          # A loop is performed for a given HISTDATE,CATEGORY,CUSKEY, for every distinct PROKEY
            For [HISLNK]KEYHIS
              # A loop is performed for every record having the same HISDATE,CATEGORY,CUSKEY,PROKEY
              # [CUST]NAME, [PROD]NAME, [SREP]NAME are available here
              ...
            Next
            ...
          Next
          ....
        Next
        ...
      Next
   Next

 # Example 3
 # A customer can have up to 2 associated sales rep or not (the REP(0..1) columns can be empty)
 # But here, we want to select only the customers that have two sales representatives
 Local File BCUSTOMER [BPC], SALESREP [SRE1], SALESREP [SRE2]

 # A not optimal link syntax would be the following:
 Link [BPC] whith [SRE1]REP0=[BPC]REP,[SRE2]REP0=[BPC]REP(1) As [LNK] Where [BPC]REP<>"" and [BPC]REP(1)<>""
 # The reason is that an external join is not optimal, and that an additional filtering condition is added

 # An optimal link syntax would be the following:
 Link [BPC] whith [SRE1]REP0~=[BPC]REP(0),[SRE2]REP0~=[BPC]REP(1) As [LNK]
 # Here, the join is faster, and the customers returned have mandatorily two existing sales representatives
```

# Description

`Link` is used to define a set of joins between a main table and additional tables, specifying any selection and sort criteria. It is also meant to define an abbreviation (that will be called the link abbreviation) to access all these tables with a single Read or For instruction. The main table and the linked tables must first have been opened with a [Local](4gl_local.html) [File](4gl_file.html) instruction.

# Comments

* You cannot perform a [Write](4gl_write.html), [Rewrite](4gl_rewrite.html), [Update](4gl_update.html) or [Delete](4gl_delete.html) instruction on an abbreviation opened with a [Link](4gl_link.html).
* The main file abbreviation and the linked table abbreviations can still be used to access independently the corresponding tables (in read or write mode) using their keys. However, only a read or a loop performed on the link abbreviation will load all the data related to the tables in the join.
* The columns read in the join are by default all the columns of the different tables. They are in the different [F] classes for every table in the join. There is no [F] nor [G] class associated with the link abbreviation.
* By default, a `select *` is done and this might bring a lot of columns if a lot of tables are in the join. To have better performances, it is recommended to use the [Columns](4gl_columns.html) instruction to have restrictions on the returned result, especially if [For](4gl_for.html) loops are done on joins made on large tables.
* The [Order By](4gl_order-by.html) clause in `Link` is used to define (or redefine) the sorting order on the join when the link abbreviation is used. For more information about [Order By](4gl_order-by.html), refer to the corresponding [documentation](4gl_order-by.html).
* The keys that can be used with the `Link` abbreviation are:

  + The key defined in the 'Order By' clause in `Link` (if there is one).
  + The key defined in the 'Order By' clause for the file, for the main file (if there is one), or the last [Filter](4gl_filter.html) performed on this file.
  + One of the keys defined for the main table.
* The [Where](4gl_where.html) clause in `Link` is used to filter the lines returned from the join. It can include conditions on all the columns included in the `Link`. It adds an additional restriction to any [Where](4gl_where.html) clauses defined on the tables in the join. For more information about [Where](4gl_where.html), and to know the functions and operators used, refer to the [Where](4gl_where.html) documentation.
* When a left outer join is performed, the tables for which no records have been found are filled with "empty" values (empty string, null numeric values and dates). Make sure that these empty values (empty strings) are, from a SQL point of view, null values, and the Sage X3 engine does not make a difference. A conflict would be the following example:

  ```
  Link [HIS] With [SREP]REPKEY   = [HIST]HISTREP  As [HHH] Where [SREP]FIELD=""
  ```

    
  If you consider this request, it will return only the [HIS] lines that are linked with a [SREP] line for which the [SREP]FIELD is empty, and not the [HIS] lines that are not linked on [SREP] (ie. the difference between strict and outer join). These lines are not considered because [SREP]FIELD, from a SQL point of view, is a null value and not an empty string.
* The abbreviation used for the link must not have been used by an already opened table (it would throw an error). The behavior of `Link` is the same as that of a [Local](4gl_local.html) File.
* Up to 8 different links may be defined for a given main table. Of course, this limit can be overwritten if the main table is opened two times with different abbreviations.
* Constants can be used in a definition of a link, for example:

  ```
  Link [CUST] With [STA]STATCODE=1;[CUST] As [STC]
  ```
* Links can be done on the same table if opened with two different abbreviations.
* A link may only be defined on tables located on the same server.
* A filter may be defined, with [Filter](4gl_filter.html) on the link abbreviation, on a join.
* The order in which the links are declared can be important, depending on the database. See the following example:

  ```
  Link [A] with [B]KEY1=[A]FIELD1,
  &               [C]KEY2=[B]FIELD2,
  &               [D]KEY3=[C]FIELD3;[A]FIELD1
  &               As [E]
  ```

    
  With SQL server, it is important to mention the link to [D] after the link to [C] because the join expression refers to a [C] field. With Oracle, you can switch the lines and the database will still be able to perform the following join:

  ```
  Link [A] with [D]KEY3=[C]FIELD3;[A]FIELD1,
  &               [C]KEY2=[B]FIELD2,
  &               [B]KEY1=[A]FIELD1
  &               As [E]
  ```

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | A linked table is not opened. |
| 20 | The main abbreviation is a link abbreviation. |
| 21 | The key does not exist on a linked table. |
| 28 | Abbreviation already used in a link condition. |

# See also

[Read](4gl_read.html), [File](4gl_file.html), [Filter](4gl_filter.html), [Order By](4gl_order-by.html), [Where](4gl_where.html), [For](4gl_for.html), [Write](4gl_write.html), [Rewrite](4gl_rewrite.html), [Delete](4gl_delete.html), [Update](4gl_update.html), [Columns](4gl_columns.html).

  

[Index](index.html)  [Home](getting-started_home.html)