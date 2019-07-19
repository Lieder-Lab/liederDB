# liederDB
A new relational database improved from MySQL.

Optimized MySQL, support middle layer modul storage, faster, more modular syntax and more optimized operation.
All elements save as String in kernel, so default element type is String.

### Grammar regulation(Different from MySQL):
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;
* '' and "" are same for liederDB;
* To be assigned elements and corresponding column names should packaged into __separated key-value pairs <>__, same as <column_name1, column_name2>, <column_value1, column_value2>.
* __No nesting allowed in <> pair.__


## Create new table with initialize columns:

__create TABLE_NAME set <COLUMNS_NAMES>__ [type <COLUMNS_TYPES>] [defaultValue <COLUMNS_defaultValues>];

* e.g.
>create Apple set <AppleName, AppleCount, AppleColor>;
>
>You would create a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.

>create Apple set <AppleName, AppleCount, AppleColor> type <string, int, string> defaultValue <'', 0, "">;
>You would create a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor with default values '', 0 and ''.
* tips
>[type <COLUMNS_TYPES>] means you can assign every column with corresponding types, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[defaultValue <COLUMNS_defaultValues>] is default value of every column when you insert a new row without assignment.


## Insert a new row into exsited table:

__insert TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES>;__

* e.g.
>insert Apple set <AppleName, AppleCount, AppleColor> = <Red Fuji, 5, red>;
>
>You would have a table with a row <Red Fuji, 5, red>.
