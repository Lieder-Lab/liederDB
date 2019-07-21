# liederDB
A new relational database improved from MySQL.

Optimized MySQL, support middle layer storage modul, faster and more optimized operation.


### Grammar regulation:
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;
* string type element don't need be enclosed in quotation marks ('' or "");
* '' and "" are same for liederDB;
* Elements to be assigned and corresponding column names should packaged into __separated key-value pair and enclosed in angle brackets <>__, same as <column_name1, column_name2>, <column_value1, column_value2>;
* The brackets () only indicate 
* Keywords are not case sensitive;
* All elements save as String in kernel, so default element type is String.
* __No nesting allowed in <> pair.__


## Create new table with initialize columns:

__create TABLE_NAME set <COLUMNS_NAMES>__ [type <COLUMNS_TYPES>] [defaultValue <COLUMNS_defaultValues>];

* e.g.
>_create Apple set <AppleName, AppleCount, AppleColor>;_
>
>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.

>_create Apple set <AppleName, AppleCount, AppleColor> type <string, int, string> defaultValue <'', 0, "">;_
>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor with type string, int ,string and with default values '', 0 and ''.

* tips
>[type <COLUMNS_TYPES>] means you can assign every column with corresponding type, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[defaultValue <COLUMNS_defaultValues>] is default value of every column when you insert a new row without assignment.


## Insert a new row into exsited table:

__insert TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES>;__

* e.g.
>insert Apple set <AppleName, AppleCount, AppleColor> = <Red Fuji, 5, red>;
>
>You would have a table with a row <Red Fuji, 5, red>.
