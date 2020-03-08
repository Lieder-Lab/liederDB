# liederDB


># News
>
>____
>2020/3/7
>>### __Now, You Can Satrt Transforming MySql / SQL Statement To LiederDB Statement In Just In Few Click!__
>> Now, you can transfrom Sql or MySql statement to LiederDB statement:
>>
>> 1. Click button "statement trans" in main panel of the "liederDB_testForm.exe" to display function panel;
>> 2. Input your MySql or Sql statement into 'input' textbox, click 'trans sql to liederDB'.
>>
>> #_# What should to be aware of is that only 'select', 'insert', 'update' and 'delete' statements of MySql / Sql is supported now, more features are under development.
____
>2020/3/6
>>### __Now, You Can Carry Your Data From MySql / Sql To Your Amazing LiederDB Just In Few Click!__
>> Now, if you want to carry data from MySql or Sql database to your LiederDB, you just need:
>>
>> 1. Click button "show trans panel" in main panel of the "liederDB_testForm.exe" to display function panel;
>> 2. Click radio button "MySql" or "Sql" to switch mode if you need;
>> 3. Fill in corresponding parameters and click "trans" button.
____

A new relational database improved from MySQL.

Optimized MySQL, support middle layer storage modul, faster and more optimized operation.

### Grammar regulation:
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;
* Elements to be assigned and corresponding column names should packaged into __separated key-value pair and enclosed in angle brackets <>__ before 'where' statement('WHERE_STATEMENT'), same as <column_name1, column_name2>, <column_value1, column_value2>;
* You can choose whether string type element in angle brackets <> should be enclosed in quotation marks (' or ") or not. __If you choose not, kernel will remove all spaces in the element, so if you want to keep them, you should package whole elements in quotation marks ('' or "")__;
* Quotation marks ' and " are same for liederDB;
* The brackets () only used for function parameter, nesting or a whole 'table' statement('TABLE_STATEMENT') (there must be a table alias behind the 'table' statement, like this: (TABLE_CREATE_STATEMENT) TABLE_ALIAS) (reference to MySQL).
* Keywords are not case sensitive;
* All elements save as String in kernel, so default element type is String.
* Using brackets () to declare right order is recommended in 'where' statement especially when you rearrange the order the commend works.
* The escape character for liederDB is slash '\', only works for quotation marks `, 'and " now.
* __No nesting allowed in <> pair.__
* The spaces at the start or the end of column name or table name would be trimmed off by kernel when you create table, adjust table name, insert new column, or adjust columns.

____
## Create a new table with initializing columns:

__create TABLE_NAME set <COLUMNS_NAMES>__ [type <COLUMNS_TYPES>] [default <COLUMNS_defaultValues>] [comment <COLUMNS_COMMENTS>];__

* e.g.
>
    create Apple set <AppleName, AppleCount, AppleColor>;

>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.

* e.g.
>
    create Apple set <AppleName, AppleCount, AppleColor> type <string, int, string> defaultValue <'', 0, ""> comment <'apple name', 'apple count', 'apple color'>;

>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor with type <string, int ,string> and with default values <'', 0, ''> and comments <'apple name', 'apple count', 'apple color'>.

or

__create TABLE_NAME like IMITATED_TABLE_NAME;__
* e.g.
>
    create Banana like Apple;

>The 'create like' statement just copies the frame of the 'IMITATED_TABLE' to a new table named 'TABLE_NAME' without table name and any content. So you have created an empty table named Banana which has 3 columns named separately AppleName, AppleCount and AppleColor same as existed Apple table, but don't have any content.

or

__create TABLE_NAME copy IMITATED_TABLE_NAME;__

or

__create TABLE_NAME copy (TABLE_STATEMENT) IMITATED_TABLE_NAME;__
* e.g.
>
    create Banana copy Apple;

>The 'create copy' statement copies the whole of the existed 'IMITATED_TABLE' to a new table named 'TABLE_NAME' contains the content. So you have created a table named Banana which has 3 columns named separately AppleName, AppleCount and AppleColor and be with the content same as existed Apple table, just have different table names.
>
>Also, you can put a TABLE_STATEMENT before the 'IMITATED_TABLE_NAME' enclosed by brackets '()' to generate the new imitated table.


* tips
>[type <COLUMNS_TYPES>] means you can assign every column with corresponding type, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[default <COLUMNS_defaultValues>] is default value of every column when you insert a new row without set any data.

____
## Insert a new row into an existed table:

__insert TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES> [, <COLUMNS_VALUES_1>, <COLUMNS_VALUES_2>...];__

* e.g.
>
    insert Apple set <AppleName, AppleCount, AppleColor> = <'Red Fuji', 5, red>;
>
    insert Apple set <AppleName, AppleCount, AppleColor> = <'Red Fuji', 5, red>, <'Yellow Banana', 5, green>;

>You would have inserted the data of one new row or more than one new row into the 'Apple' table.

____
## Update some existed elements in table:

__update TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES> [where statement];__

* e.g.
>
    update Apple set <AppleColor> = <green> where AppleCount = 3 and AppleName = Red Fuji;

>Now you updated the AppleColor value where AppleCount = 3 and AppleName = Red Fuji;
>
>The 'where' statement is not mandatory, specifies the constraints of the preceding statement. More details for 'where' statement, please see the following chapter.

### some operation marks: ++ / -- / += / -=

* e.g.
>
    update Apple set <AppleCount> = <++> where AppleName = Red Fuji;
>
    update Apple set <AppleCount, AppleColor> = <--. green> where AppleName = Red Fuji;
>
    update Apple set <AppleColor, AppleCount> = <green, +=3.0> where AppleCount = 3 and AppleName = Red Fuji;

>If you repleace some COLUMNS_VALUEs in <COLUMNS_VALUES> with the operation mark, value in corresponding column would be self-increased or self-decreased.
>
>What should be noticed is that '++' and '--' only work for numerical value, '+=' for string value means 'append', '-=' for string value means remove corresponding characters in the string. Of course, '+=' and '-=' for numerical value is worked as numerical operations also.

____
## Delete some existed rows of table:

__delete TABLE_NAME [where statement];__

__delete TABLE_NAME at [first__(default), __last] ROW_INDEX / [ROW_INDEXES];__ 

__delete TABLE_NAME [from [first__(default), __last] start_ROW_INDEX] [to  [first__(default), __last] end_ROW_INDEX]__ (index starts from 1)

* e.g.
>
    delete Apple where AppleCount = 3 and AppleName = Red Fuji;
>
    delete Applt at 1;
>
    delete Applt at last 2;
>
    delete Apple at [2, 3, 4];
>
    delete Apple from 1 to last 3;
>
    delete Apple from last 2;

>The 'delete' statement just means remove the data of some rows from a existed table, or clear whole table, not remove whole table (remove whole table see 'remove' statement). For the unity of grammar, it writied as 'delete TABLE_NAME' instead of 'delete from TABLE_NAME';
>
>Now you removed the row where AppleCount = 3 and AppleName = Red Fuji or removed some rows in 'at substatement';
>
>The 'where substatement' and the 'at substatement' are not mandatory. commend without both 'where substatement' and 'at substatement' means clear all elements of the table.
>
>For 'at substatement', 'at ROW_INDEX' means delete row which index == ROW_INDEX; 'at last ROW_INDEX' means delete row which index == ROWS_COUNT - ROW_INDEX + 1 if this row existed; 'at [ROW_INDEXES]' means delete rows which index in array [ROW_INDEXES].
>
>For 'from / to substatement', means a range of row to delete. The 'start_ROW_INDEX' is start, and the 'end_ROW_INDEX' is end, 'first / last' is available for 'start_ROW_INDEX' and 'end_ROW_INDEX', as same, 'first' is default.

____
## Remove an existed table:


__remove TABLE_NAME;__

* e.g.
>
    remove Apple;

>You would remove whole table named Apple.

____
## Select data from some tables:

__select [distinct__ (default) __/ all] * from TABLE_NAME [where statement];__

__select [distinct__ (default) __/ all] <COLUMNS_NAMES_1, COLUMNS_NAMES_2> from TABLE_NAME [where statement];__

* e.g.
>
    select * from Apple;
>
    select all * from Apple;
>
    select <AppleColor, AppleCount> from Apple where AppleCount = 3;

>Now you got data of Apple as you want to;
>
>The 'where' statement is not mandatory.
>
>The [distinct (default) / all] is optional, absence or 'distinct' means this SELECT_STATEMENT just returns distinct result, 'all' means returns all result.
____

## Adjust some property of table:

### Update Table Name

>__adjust TABLE_NAME update table set name = TABLE_NEW_NAME__
>
>* e.g.
>>
>       adjust Apple update table set name = 'NewApple';
>
>Now you updated the name of table 'Apple' as 'NewApple'.

### Add New Column

>__adjust TABLE_NAME add column set name = COLUMN_NEW_NAME [,type = COLUMN_NEW_TYPE] [,default = COLUMN_NEW_DEFAULT] [,comment = COLUMN_NEW_COMMENT] [,position = COLUMN_NEW_INDEX / position before REFERENCE_COLUMN_NAME / position after REFERENCE_COLUMN_NAME]__
>
>* e.g.
>>
>       adjust Apple add column set name = 'AppleSource', type = 'string', comment = 'Source of apple.', default = 'China'£¬ position after 'AppleName';
>
>Now you added a new column named 'AppleSource', default value is 'China', type is 'string' and comment is 'Source of apple.'.

### Update Column Structure

>__adjust TABLE_NAME update column COLUMN_NAME set [name = COLUMN_NEW_NAME] [,type = COLUMN_NEW_TYPE] [,default = COLUMN_NEW_DEFAULT] [,comment = COLUMN_NEW_COMMENT] [,position = COLUMN_NEW_INDEX / position before REFERENCE_COLUMN_NAME / position after REFERENCE_COLUMN_NAME]__
>
>__adjust TABLE_NAME update column index COLUMN_INDEX set [name = COLUMN_NEW_NAME] [,type = COLUMN_NEW_TYPE] [,default = COLUMN_NEW_DEFAULT] [,comment = COLUMN_NEW_COMMENT] [,position = COLUMN_NEW_INDEX / position before REFERENCE_COLUMN_NAME / position after REFERENCE_COLUMN_NAME]__
>
>* e.g.
>>
>       adjust Apple update column AppleCount set name = 'apple count', default = 'red', comment = 'All apples are red.', position after AppleName;
>>
>       adjust Apple update column index 3 set name = 'apple count', default = 'red', comment = 'All apples are red.', position = 2;
>
>Now you reset the name, default value, comment and position of the column named 'AppleCount' before.
>
>The 'COLUMN_INDEX' and 'COLUMN_NEW_INDEX' should be an integer, start from 1 without 0.

### Remove Existed Column

>__adjust TABLE_NAME remove column COLUMN_NAME__
>
>__adjust TABLE_NAME remove column index COLUMN_INDEX__
>
>* e.g.
>>
>       adjust Apple remove column AppleCount;
>>
>       adjust Apple remove column index 3;
>
>Now you removed the column named 'AppleCount' or index 3.

____
## Where statement:
### and / or

>#### __and__
>__CONDITIONS_1 and CONDITIONS_2__
>
>* e.g.
>>
>       where __AppleCount = 1 and AppleColor = red__ and/or ...
>
>>The 'and' substatement returns the result meet __CONDITIONS_1 and CONDITIONS_2__ simultaneously;
>
>#### __or__
>__CONDITIONS_1 or CONDITIONS_2__
>
>* e.g.
>>
>       where __AppleCount = 1 or AppleColor = red__ and/or ...
>
>>The 'or' substatement returns the result meet __CONDITIONS_1 or CONDITIONS_2__;
>
>_The 'and' substatement and 'or' substatement are on the same grammatical levels in 'where' statement, but 'and' substatement has a higher priority than 'or' substatement. Kernel would  process all 'and' statements first and then process the 'or' substatement later, if commend designed not follow this order, please use brackets () to declare the right order, as we recommend already._

### LOGICAL_OPERATORS:  =    ==    >    <    >=    <=    !=

>#### __=    ==    !=__
>__object_1 LOGICAL_OPERATORS object_2__
>
>* e.g.
>>
>       where AppleCount = 1
>>
>       where AppleCount != 1
>
>>'=' and '==' are same for liederDB, check whether object_1 and object_2 are equal;
>>
>>'!=' checks whether object_1 and object_2 are not equal;
>>
>>'=', '==' and '!=' can be used for all types of objects;
>
>#### __>    <    >=    <=__
>__number_1 LOGICAL_OPERATORS number_2__
>
>* e.g.
>>
>       where AppleCount > 1
>>
>       where AppleCount <= 1
>
>>The role of these symbols is the same as their meaning in mathematics;
>>
>>However, it should be noted that these symbols can only be used when both sides are all numbers, otherwise the kernel will report an error.

### in
>#### TABLE statement
>__left_element in ('select' statement_single_column) SELECTED_TABLE_ALIAS__
>
>or
>
>__left_element in ('select' statement) SELECTED_TABLE_ALIAS[SINGLE_COLUMN_NAME]__
>
>or
>
>__left_element in EXISTED_TABLE[SINGLE_COLUMN_NAME]__
>
>* e.g.
>
>(1)
>>
>       where AppleCount in (select count from CountList) countTable 
>(2)
>>
>       where AppleCount in (select * from CountList) countTable[count]
>(3)
>>
>       where AppleCount in CountList[count]
>
>> The 'table' statement behind 'in' called 'in table' statement only used for selected or existed table;
>>
>> What should be noticed is that __the 'in table' statement only work for data of single column__, so the selected or existed table must have only one column, or you can declare one column through declaring the column name after the table name packaged by brackets '[ ]' from the table which contains more than one columns like .e.g (2) or (3);
>>
>> If you use 'select' statement in 'in table' statement, the brackets '( )' and the table alias are mandatory;
>>
>> The 'in table' statement returns whether the left element appered in the column of the table.
>
>#### [ ] statement
>__left_element in [element_1, element_2, element_3,  ...]__
>
>* e.g.
>>
>       where AppleCount in [1,2,3]
>
>>For liederDB, '[ ]' means an array, elements in this array should be separated by ',';
>>
>>The 'in [ ]' statement returns whether the left_element appered in the right array;
>>
>>The function of this statement is covered by 'like' statement shown below actually, about more please see the 'like' statement.

### like
>#### SINGLE_ELEMENT statement
>__LEFT_ELEMENT like LIKE_EXPRESSION__
>
>* signs of like_expression
>>
>> _'___' represents arbitrary a character_;
>>
>> '%' represents any number (including 0) of arbitrary characters;
>* e.g.
>>
>       where AppleName like 'R&%d %j'
>
>>Of course, 'Red Fuji' meet this expression.
>#### [ ] ( / ![ ]) statement
>__left_element like [like_expression_1, like_expression_2, ...] / ![like_expression_1, like_expression_2, ...]__
>
>* e.g.
>>
>       where AppleName like [R%d %j, Re% F%i]
>
>>[ ] ( or ![ ] ) means an array, contain some like_expressions;
>>
>>'[ ]' statement in 'like' statement returns whether the left_element meet any like_expression in the [ ] array;
>>
>>'![ ]' statement in 'like' statement will return true if the left_element not meet any like_expression in the [ ] array;

----

## Some Optional Substatements:

### order by

(Only for 'select' statement and 'update' statement)

__TABLE_STATEMENT order by TABLE_COLUMN_NAME [desc / asc__ (default) __] [number]__

* e.g.
>
    update Apple order by AppleColor
>
    update Apple order by AppleCount desc number
>
    select * from Apple order by AppleColor asc
>
    select AppleColor, AppleCount from Apple order by AppleCount number

>The keyword pair 'desc / asc' means 'descending' and 'ascending', and 'asc' is default when you miss indicating them.
>
>The keyword 'number' indicates the way the table sorted by, digital or dictionary. Of course, 'number' means digital sort, and missing 'number' means dictionary sort. What should to be aware of is that digital sort only works when all element of the 'TABLE_COLUMN' is digital.
>
>In 'update' statement, 'order by' would sort whole table order by table column named TABLE_COLUMN_NAME.

### skip / limit

(Only for 'select' statement)

__SELECT_STATEMENT [skip SKIP_COUNT] [limit LIMIT_COUNT]__

* e.g.
>
    select * from Apple skip 1;
>
    select * from Apple skip 1 limit 2;
>
    select * from Apple limit 2;

>The keyword 'skip' and the SKIP_COUNT behind it mean remove / skip the first SKIP_COUNT rows of the result data.
>
>The keyword 'limit' and the LIMIT_COUNT behind it mean only take the first LIMIT_COUNT rows of the remaining result data.
>
>What should be noticed is that the SKIP_COUNT and LIMIT_COUNT must be positive, otherwise this statement will not work. 
>
>One SELECT_STATEMENT could only contain one LIMIT_STATEMENT and one SKIP_STATEMENT, if you need some complex skip or limit statement, you can consider using SELECT_STATEMENT nesting.

### ELEMENT_FUNCTION: count / sum / max / min / avg / first / last

(Only for 'select' statement)

__select <ELEMENT_FUNCTION(* / COLUMN_NAME)> from TABLE_NAME__

* e.g.
>
    select <count(AppleColor)> from Apple;
>
    select <count(*)> from Apple;
>
    select <max(AppleCount), AppleColor> from Apple;
>
    select <AppleName, first(AppleColor)> from Apple where AppleCount > 2;

>The 'ELEMENT_FUNCTION' are functions with only one result, and will fill the result into every cell of corresponding column.
>
>>The 'count' function return the selected row count of the column named 'COLUMN_NAME' from the result table.
>
>>The 'sum' function sums the numerial value of the column named 'COLUMN_NAME' from the result table.
>
>>The 'max' or 'min' function returns the max or min numerial value of the column named 'COLUMN_NAME' from the result table.
>
>>The 'avg' function returns the average numerial value of the column named 'COLUMN_NAME' from the result table.
>
>>The 'first' or 'last' function returns the first or last value of the column named 'COLUMN_NAME' from the result table.
>
>What should be noticed is that functions 'sum / max / min / avg' only work for numerial value.
----

## Setup some features for kernel

### runMode (only for non-virtual memory technology)
__setup runMode hardSpeed__ / __setup runMode balance__ / __setup runMode smoothBalance__ (detault) / __setup runMode memorySave__
>Four main 'runMode's substatements mean different balances between the speed and the memory cost of the kernel running for non-virtual memory technology.
>
>The 'hardSpeed' means the fastest speed. Every table would be stored on memory (RAM), so if you have too much data of tables more than the memory could bear for non-virtual memory technology, this 'runMode' may cause some memory crashes. So for non-virtual memory technology, unless you have enough memory for your data of tables, this 'runMode' would not be recommended most, for virtual memory technology, the 'hardSpeed' is the best choice for all.
>
>The 'balance' means a balance way of the kernel running. Every table would be stored in memory (RAM) at first, but if it don't have enough memory to save all tables, kernel will transfer all tables into hard disk, and if you need read or write some data of some tables again, those tables would be moved to RAM one by one again. So the 'runMode' may spend more time than the 'hardSpeed' one, but this only occurs when memory (RAM) is not enough for your data. Other than this, the 'balance' has almost as fast as the 'hardSpeed'. So the 'balance' is recommended most. The other version of the 'balance' can refer to the 'smoothBalance'.
>
>The 'smoothBalance' is similar to the 'balance' one, the difference is the way to handle memory warning. That is when memory don't have enough memory to put all tables, kernel will transfer tables into hard disk one by one without all tables one-off until move out enough space to work. So the 'smoothBalance' kept fast in case of security greatly.
>
>The 'memorySave' means all data would be saved on the hard disk after every operation, so this 'runMode' means the slowest speed and the minimum memory storage (although it won't be particularly slow, but it means more times hard disk reads and writes, it depends on the hard disk read and write speed of your hardware).

### efficientMode
__setup efficientMode true__ / __setup efficientMode false__ (detault)
>The 'efficientMode' substatement used in high-density instruction situations makes kernel try to store data of tables with another thread rather than main thread. 
>
>But what should be awared is that more threads work means more thread overhead, there may not be so particularly desirable performance when the amount of data in a single table is not very huge (such as less than 1 billion bytes). Of course, by binary storage, you can get a very quick storage performance without turning on the 'efficientMode' also.
>
>The 'efficientMode' need more memory space, and if memory space is not enough for 'efficientMode', 'efficientMode' while turn off automatically until memory space back to normal.
>
>So the 'efficientMode' just recommended opened in huge amount of data and high frequencies operation situation to get a little faster than the regular method.

### savePath
__setup savePath TABLES_SAVE_FOLDER_PATH [copy]__ (default) / __setup savePath TABLES_SAVE_FOLDER_PATH move__
>The 'savePath' substatement is used when you want to set or switch the path of folder where the tables stored on the hard disk.
>
>The 'TABLES_SAVE_FOLDER_PATH' is the path of folder where you want to store the tables.
>
>The keyword 'copy' behind 'TABLES_SAVE_FOLDER_PATH' means when you switch the folder path, data in old folder will copy to the new one;
the 'move' means move to the new one (delete from the old one).

____
## Show something
__show tables / show config__
>The 'show tables' statement would sync all tables between memory and hard disk, and assemble a table with names of all tables.
>
>The 'show config' statement would assemble a table with all configs.

___
## More questions and suggestions
If you have more questions or some suggestions, please email to 357274178@qq.com. It's my pleasure to talk with you about this.
