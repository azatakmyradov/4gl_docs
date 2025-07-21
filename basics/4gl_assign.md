[Index](index.html)  [Home](getting-started_home.html)

Assign

`Assign` is an instruction that allows you to perform an assignment to a variable whose name is calculated.

# Syntax

```
Assign NAME_EXPR With VALUE_EXPR
```

* `NAME_EXPR` is the expression giving the name of the variable to assign.
* `VALUE_EXPR` is the value to be assigned.

# Examples

```
# 5 variables AMOUNT1 to AMOUNT5 have to be assigned from values found in an array (ARRAY_AMT)
Local Integer I
Local Decimal AMOUNT1, AMOUNT2, AMOUNT3, AMOUNT4, AMOUNT5

  For I=1 to 5
    Assign "AMOUNT"+num$(I) with ARRAY_AMT(I)
  Next I
```

```
## For a given table record, let's assign randomly values and insert several lines

# Step 1 : declarations
Local File MYTABLE [MYT]
Local Integer I
Local Integer TYP(1..[G:MYT]nbzon-1)

# Step 2 : Analyze types for assignment
  For I=1 to dim(TYP)
    TYP(I)=evalue("type([MYT]"+[G:MYT]adxfname(I)+")")
    # TYP=10 for strings, TYP=1,2,3,4 for the corresponding types, TYP=5 for decimals, TYP=0 otherwise
    If TYP(I)>265 : TYP(I)=0
    Elsif TYP(I)>10 : TYP(I)=10
    Elsif find(TYP(I),5,6,7) : TYP(I)=5
    Endif
  Next I

# Step 3 : Create 20 random records
  Trbegin [MYT]
  For I=1 to 20
    Gosub CREATE_RANDOM_RECORD
  Next I
  Commit
End

# The sub-program that assigns random values
# The random value type depends on the type computed before
$CREATE_RANDOM_RECORD
  For I=1 to [G:MYT]nbzon-1
    For J=0 to evalue("dim([MYT]"+[G:MYT]adxfname(I)+")")
      Case TYP(I)
        When 1 : Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With int(rnd(255))
        When 2 : Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With int(rnd(32767))
        When 3 : Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With [1/1/1970]+int(rnd(36500))
        When 4 : Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With int(rnd(2^31-1))
        when 5 : Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With rnd(10^10)
        when 10: Assign "[MYT]"+[G:MYT]adxfname(I)+"("+num$(J)+")" With sigma(1,int(rnd(20)),chr$(65+int(rnd(26))))
      Endcase
    Next j
  Next I
  Write [MYT]
Return
```

# Comments

The type of assignment value must be consistent with that of the variable to be assigned.

The variable to be assigned must exist.

The `assign` instruction does not assign a group of variables (for example, the assignment type from class to class).

# See also

[evalue](4gl_evalue.html).

  

[Index](index.html)  [Home](getting-started_home.html)