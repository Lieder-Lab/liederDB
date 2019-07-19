# liederDB
A new relational database improved from MySQL.

Optimized MySQL, support middle layer modul storage, faster, more modular syntax and more optimized operation.
All elements save as String in kernel, so default element type is String.

### Grammar regulation(Different from MySQL):
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;



## Create new table with initialize columns:

__create TABLE_NAME set <COLUMNS_NAME>__ [type <COLUMNS_TYPE>] [defaultValue <COLUMNS_defaultValue>];

* e.g.
>create Apple set <AppleName, AppleCount, AppleColor>;
>
>You would create a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.
>
>create Apple set <AppleName, AppleCount, AppleColor>;
* tips
>[type <COLUMNS_TYPE>] means you can assign every column with corresponding types, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[defaultValue <COLUMNS_defaultValue>] is default value of every column when you insert a new row without assignment.


## Insert a new row into exsited table:

insert
