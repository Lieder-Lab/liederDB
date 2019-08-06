# liederDB
A new relational database improved from MySQL.

Optimized MySQL, support middle layer storage modul, faster and more optimized operation.


### Grammar regulation:
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;
* Elements to be assigned and corresponding column names should packaged into __separated key-value pair and enclosed in angle brackets <>__ before 'where' statement, same as <column_name1, column_name2>, <column_value1, column_value2>;
* You can choose whether string type element in angle brackets <> should be enclosed in quotation marks ('' or "") or not. __If you choose not, kernel will remove all spaces in the element, so if you want to keep them, you should package whole elements into quotation marks ('' or "")__;
* Quotation marks '' and "" are same for liederDB;
* The brackets () only indicate function parameter or a whole table expression (there must be a table alias behind the table expression, like this: (TABLE_CREATE_EXPRESSION) TABLE_ALIAS) (reference MySQL).
* Keywords are not case sensitive;
* All elements save as String in kernel, so default element type is String.
* Using brackets () to declare right order is recommended in where statement especially when you are due to the order the commend works.
* __No nesting allowed in <> pair.__

>__Art of Nesting (Table statement)__
>
>The key words like 'create', 'insert', 'update', 'delete', 'select' are called pass-value key words, the statement guided by these words called the 'Table statement'. And those 'Table statement' would return a result table as the result of calculation of the statement whatever you need them or not.
>
>If you want to use those result tables in other statements, just make the 'Table statement' enclosed by the brackets '()' and attach a alias behind the 'Table statement' and nest them into the other statements. You would use the result table through it's alias. ( What should to be aware of is the alias of the new table cannot be equal to any exsiting table's name. )
>
>Looks like: "create a copy __(create b set <q,w,e,r,t>) s__" or "create a copy __(create b set <q,w,e,r,t>) b__" ( see below for more about 'copy statement' ). You would get two tables called 'a' and 'b' ( at the first sentence, because 's' is an alias, so 's' would't be saved as a normal table, which would be removed from memory after operation ).



____
## Create a new table with initialize columns:

__create TABLE_NAME set <COLUMNS_NAMES>__ [type <COLUMNS_TYPES>] [default <COLUMNS_defaultValues;__

* e.g.
>
>_create Apple set <AppleName, AppleCount, AppleColor>;_

>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.

* e.g.
>
>_create Apple set <AppleName, AppleCount, AppleColor> type <string, int, string> defaultValue <'', 0, "">;_

>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor with type string, int ,string and with default values '', 0 and ''.

or

__create TABLE_NAME like IMITATED_TABLE_NAME;__
* e.g.
>
>_create Banana like Apple;_

>The 'create like' statement just copies the frame of the 'IMITATED_TABLE' to a new table named 'TABLE_NAME' without table name and any content. So you have created an empty table named Banana which has 3 columns named separately AppleName, AppleCount and AppleColor same as exsited Apple table, but don't have any content.

or

__create TABLE_NAME copy IMITATED_TABLE_NAME;__

or

__create TABLE_NAME copy (TABLE_STATEMENT) IMITATED_TABLE_ALIAS;__
* e.g.
>
>_create Banana copy Apple;_
>
>_create Banana copy (select * from Apple) s;_

>The 'create copy' statement copies the whole of the exsited 'IMITATED_TABLE' to a new table named 'TABLE_NAME' contains the content. So you have created a table named Banana which has 3 columns named separately AppleName, AppleCount and AppleColor and be with the content same as exsited Apple table, just have different table names.
>
>Also, you can put a TABLE_STATEMENT before the 'IMITATED_TABLE_NAME' / 'IMITATED_TABLE_ALIAS' enclosed by brackets '()' to generate the new imitated table.
>
>If you used the last method to create new table with 'TABLE_STATEMENT', the 'IMITATED_TABLE_ALIAS' shouldn't be forgotten.


* tips
>[type <COLUMNS_TYPES>] means you can assign every column with corresponding type, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[default <COLUMNS_defaultValues>] is default value of every column when you insert a new row without input some columns.

____
## Insert a new row into exsited table:

__insert TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES> [, <COLUMNS_VALUES_1>, <COLUMNS_VALUES_2>...];__

* e.g.
>
>_insert Apple set <AppleName, AppleCount, AppleColor> = <'Red Fuji', 5, red>;_
>
>or
>
>_insert Apple set <AppleName, AppleCount, AppleColor> = <'Red Fuji', 5, red>, <'Yellow Banana', 5, green>;_

>You would have inserted a new row or two new rows into the 'Apple' table.

____
## Update some exsited element in table:

__update TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES> where CONDITIONS;__

* e.g.
>
>_update Apple set \<AppleColor> = \<green> where AppleCount = 3 and AppleName = Red Fuji;_

>Now you updated the AppleColor value where AppleCount = 3 and AppleName = Red Fuji;
>
>CONDITIONS after 'where' is where statement(not required), specifies the constraints of the preceding statement. More about rules about where statement, please see the following chapter for details.

Some Clauses:
>
>### order by ... [asc (default) / desc] 
>__CREATE_STATEMENT order by COLUMN_NAME_a [asc (default) / desc] order by COLUMN_NAME_b [asc (default) / desc] ... ;__
>
>* e.g.
>
>>_update Apple set \<AppleColor> = \<green> where AppleCount = 3 and AppleName = Red Fuji order by AppleColor desc order by AppleCount;_
>>
>>_update Apple order by AppleColor order by AppleCount asc;_
>
>>The first example you have updated the table 'Apple' and sort by your 'order by' statements, the secord one just sort the table 'Apple';
>>

____
## Delete some exsited rows in table:

__delete TABLE_NAME where CONDITIONS;__

* e.g.
>
>_delete Apple where AppleCount = 3 and AppleName = Red Fuji;_

>Delete statement just means remove some rows from exsited table, or clear the table, not remove whole table(remove whole table see remove statement). For the unity of grammar, it writied as 'delete TABLE_NAME' instead of 'delete from TABLE_NAME';
>
>Now you removed the row where AppleCount = 3 and AppleName = Red Fuji;
>
>Where statement is not required, commend without where statement means clear all elements of the table.

____
## Remove an exsited table:


__remove TABLE_NAME;__

* e.g.
>
>_remove Apple;_

>You have removed whole table named Apple.

____
## Select data from some tables:

__select * from TABLE_NAME [where CONDITIONS];__
__select <COLUMNS_NAMES> from TABLE_NAME [where CONDITIONS];__

* e.g.
>
>_select * from Apple;_
>
>_select <AppleColor, AppleCount> from Apple where AppleCount = 3;_

>Now you got data of Apple as you want to;
>
>Where statement is not necessary.

Some Clauses:
>
>### [ left / right / inner (default) / all ] join
>select * from TABLE_1_NAME [ left / right / inner (default) / all ] join TABLE_2_NAME on TABLE_1_NAME.TABLE_1_COLUMN_NAME = TABLE_2_NAME.TABLE_2_COLUMN_NAME;
>
>select <COLUMNS_NAMES> from TABLE_1_NAME [ left / right / inner (default) / all ] join TABLE_2_NAME on TABLE_1_NAME.TABLE_1_COLUMN_NAME = TABLE_2_NAME.TABLE_2_COLUMN_NAME;
>
>* e.g.
>
>>_select * from Apple left join Banana on Apple.AppleColor = Banana.BananaColor;_
>>
>>_select <AppleColor, BananaCount> from Apple join Banana on Apple.AppleCount = Banana.BananaCount;_
>
>>Now you got a joined table. The effect of 'join statement' please refer to MySQL.
>
>### [ distinct (default) / all ] union
>select * from TABLE_1_NAME [ distinct (default) / all ] union TABLE_2_NAME;
>
>select <COLUMNS_NAMES> from TABLE_1_NAME [ distinct (default) / all ] union TABLE_2_NAME;
>
>* e.g.
>
>>_select * from Apple union Banana;_
>>
>>_select <AppleColor, BananaCount> from Apple all union Banana;_
>
>>Now you got a unioned table. The effect of 'join statement' please refer to MySQL.
>>
>>What should be awared is TABLE_1_NAME and TABLE_1_NAME in 'union statement' should have the same columns struct.
>
>### order by ... [asc (default) / desc]
>select * / <COLUMNS_NAMES> from TABLE_NAME order by COLUMN_NAME_a [asc (default) / desc] order by COLUMN_NAME_b [asc (default) / desc] ... ;
>
>* e.g.
>
>>_select * from Apple order by AppleColor desc order by AppleCount;_
>>
>>_select <AppleColor, AppleCount> from Apple order by AppleColor order by AppleCount asc;_
>
>>Now you got a table ordered by some columns. Kernel would order original table by COLUMN_NAME_a and COLUMN_NAME_b and COLUMN_NAME_c ... ;
>>
>>What should be awared is TABLE_1_NAME and TABLE_1_NAME in 'union statement' should have the same columns struct.
>
>### count(COLUMN_NAME) 
>select <count(COLUMN_NAME) [, COLUMNS_NAMES ] > from TABLE_STATEMENT ;
>
>* e.g.
>
>>_select <count(AppleColor)> from where AppleCount = 2;_
>>
>>_select <count(*), AppleColor> from where AppleCount = 2;_
>
>>Now you have got a table including some count or columns you want.
____
## Where statement:
### and / or

>#### __and__
>__CONDITIONS_1 and CONDITIONS_2__
>
>* e.g.
>>
>>_where AppleCount = 1 and AppleColor = red and/or ..._
>
>>The 'and' sub statement returns the result meet __CONDITIONS_1 and CONDITIONS_2__ simultaneously;
>
>#### __or__
>__CONDITIONS_1 or CONDITIONS_2__
>
>* e.g.
>>
>>_where AppleCount = 1 or AppleColor = red and/or ..._
>
>>'or' sub statement returns the result meet __CONDITIONS_1 or CONDITIONS_2__;
>
>_The 'and' sub statement and 'or' sub statement are on the same grammatical levels in where statement, but 'and' sub statement has a higher priority than 'or''s. Kernel would  process all 'and' statements first and then process the 'or's later, if commend designed not follow this order, please use brackets () to declare the right order, as we recommend already._

### LOGICAL_OPERATORS:  =    ==    >    <    >=    <=    !=

>#### __=    ==    !=__
>__object_1 LOGICAL_OPERATORS object_2__
>
>* e.g.
>>
>>_where AppleCount = 1_
>>
>>_where AppleCount != 1_
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
>>_where AppleCount > 1_
>>
>>_where AppleCount <= 1_
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
>__left_element in EXSITED_TABLE[SINGLE_COLUMN_NAME]__
>
>* e.g.
>>
>>_where AppleCount in (select count from CountList) countTable_ (1)
>>
>>or
>>
>>_where AppleCount in (select * from CountList) countTable[count]_ (2)
>>
>>or
>>
>>_where AppleCount in CountList[count]_ (3)
>
>> TABLE statement means there must be a selected or exsited table followed behind 'in';
>>
>> What should noticed is __this statement only work for data of single column__, so the selected or exsited table must have only one column, or you can declare one column from the table which contains more than one columns through declaring the column name after table name and packaged by brackets '[]' like (2) or (3);
>>
>> If use 'select' statement in TABLE statement, brackets '()' and table alias are mandatory;
>>
>> TABLE statement returns whether the left element appered in the column of the table.
>#### [] statement
>__left_element in [element_1, element_2, element_3,  ...]__
>
>* e.g.
>>
>>_where AppleCount in [1,2,3]_
>
>>[] means an array, elements in this array should be separated by ',';
>>
>>'in[]' returns whether the left_element appered in the right array;
>>
>>This statement works like 'like' statement shown below, about more please see the 'like' statement.

### like
>#### SINGLE_ELEMENT statement
>__left_element like like_expression__
>
>* signs of like_expression
>>
>> _'___' represents an arbitrary character_;
>>
>> '%' represents any number(including 0) of arbitrary characters;
>* e.g.
>>
>>_where AppleName like R&%d %j_
>
>>Of course, 'Red Fuji' meet this expression.
>#### [] ( / [^ ]) statement
>__left_element like [like_expression_1, like_expression_2, ...]/[^like_expression_1, like_expression_2, ...]__
>
>* e.g.
>>
>>_where AppleName like [R%d %j, Re% F%i]_
>
>>[] ( or [^ ] ) means an array, contain some like_expressions;
>>
>>'[]' statement in 'like' statement returns whether the left_element meet any like_expression in the [] array;
>>
>>'[^ ]' statement in 'like' statement will return true if the left_element not meet any like_expression in the [] array;

## Setup some features of kernel
____
### runMode
__setup runMode hardSpeed__ / __setup runMode balance__ / __setup runMode smoothBalance__ (detault) / __setup runMode memorySave__
>Three main 'runMode's mean different balances between the speed and the memory cost of the kernel running.
>
>The 'hardSpeed' means the fastest speed. Every table would be stored on memory (RAM), so if you have too much data of tables more than the memory could bear, this 'runMode' may cause some memory crashes. Unless you have enough memory for your data of tables, this 'runMode' would not be recommended most.
>
>The 'balance' means a balance way of the kernel running. Every table would be stored in memory (RAM), but if it don't have enough memory to save all tables, kernel will transfer some tables into hard disk. Of course, if you need those tables transferred in the hard disk again, the 'runMode' may spend more time than the 'hardSpeed' one. But this only occurs when memory (RAM) is not enough for your data, other than this, the 'balance' has almost as fast as the 'hardSpeed'. So the 'balance' is recommended most. The upgrade version of the 'balance' can refer to the 'smoothBalance'.
>
>The 'smoothBalance' is similar to the 'balance' one, the difference is the way to handle memory warning. That is when it don't have enough memory to save all tables, kernel will transfer some tables into hard disk one by one until move out enough space to run. So the 'smoothBalance' kept fast in case of security greatly. So the 'balance' is recommended most.
>
>The 'memorySave' means all data would be saved on the hard disk after every operation, so this 'runMode' means the slowest speed and the minimum memory storage (although it won't be particularly slow, but it means more times hard disk reads and writes, it depends on the hard disk read and write speed of your hardware).

### efficientMode
__setup efficientMode true__ / __setup efficientMode false__ (detault)
>The 'efficientMode' used in high-density instruction situations makes kernel try to store data of tables with another thread without main thread. 
>
>But what should be awared is that more threads work means more thread overhead, there may not be so particularly desirable performance when the amount of data in a single table is not very huge (such as lease than 1 billion bytes). Of course, due to the binary storage, you can get a very quick storage performance without turning on the 'efficientMode' also.
>
>The 'efficientMode' need more memory space, and if memory space is not enough for 'efficientMode', 'efficientMode' while turn off automatically until memory space back to normal.
>
>So the 'efficientMode' just recommended opened in huge amount of data and high frequencies operation situation to get a little faster than the regular method.

### savePath
__setup savePath TABLES_SAVE_FOLDER_PATH [copy]__ (default) / __setup savePath TABLES_SAVE_FOLDER_PATH move__
>The 'savePath' used when you want to set or change the folder path tables saved on hard disk.
>
>TABLES_SAVE_FOLDER_PATH is the path of folder, it could be any file path.
>
>The 'copy' behind 'TABLES_SAVE_FOLDER_PATH' means when you change the folder path, data in old folder will copy to the new one, of course, 'move' means moving to the new one (delete from the old one).

____
## More questions and suggestions
If you have more questions or suggestions, please email to 357274178@qq.com. It's my pleasure to get your email.
