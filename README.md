# liederDB
A new relational database improved from MySQL.

Optimized MySQL, support middle layer storage modul, faster and more optimized operation.


### Grammar regulation:
* <ARRAY_NAME> means <1st, 2nd, 3rd, ...>;
* There should be a ';' between every two commends to separate them;
* string type element don't need be enclosed in quotation marks ('' or "");
* '' and "" are same for liederDB;
* Elements to be assigned and corresponding column names should packaged into __separated key-value pair and enclosed in angle brackets <>__ before 'where' statement, same as <column_name1, column_name2>, <column_value1, column_value2>;
* The brackets () only indicate function parameter or a whole table expression (there must be a table alias behind the table expression, like this: (TABLE_CREATE_EXPRESSION) TABLE_ALIAS) (reference MySQL).
* Keywords are not case sensitive;
* All elements save as String in kernel, so default element type is String.
* Using brackets () to declare right order is recommended in where statement especially when you are due to the order the commend works.
* __No nesting allowed in <> pair.__


## Create a new table with initialize columns:

__create TABLE_NAME set <COLUMNS_NAMES>__ [type <COLUMNS_TYPES>] [default <COLUMNS_defaultValues>];

* e.g.
>_create Apple set <AppleName, AppleCount, AppleColor>;_
>
>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.

>_create Apple set <AppleName, AppleCount, AppleColor> type <string, int, string> defaultValue <'', 0, "">;_
>You have created a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor with type string, int ,string and with default values '', 0 and ''.

* tips
>[type <COLUMNS_TYPES>] means you can assign every column with corresponding type, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length;
>
>[default <COLUMNS_defaultValues>] is default value of every column when you insert a new row without input some columns.


## Insert a new row into exsited table:

__insert TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES>;__

* e.g.
>insert Apple set <AppleName, AppleCount, AppleColor> = <Red Fuji, 5, red>;
>
>You would have inserted a new row <Red Fuji, 5, red>.

## update some exsited element in table:

__update TABLE_NAME set <COLUMNS_NAMES> = <COLUMNS_VALUES> where CONDITIONS;__

* e.g.
>_update Apple set <AppleColor> = <green> where AppleCount = 3 and AppleName = Red Fuji;_
>Now you updated the AppleColor value where AppleCount = 3 and AppleName = Red Fuji;
>CONDITIONS after 'where' is where statement(not required), specifies the constraints of the preceding statement. More about rules about where statement, please see the following chapter for details.

## delete some exsited rows in table:

__delete TABLE_NAME where CONDITIONS;__

* e.g.
>_delete Apple where AppleCount = 3 and AppleName = Red Fuji;_
>Delete statement just means remove some rows from exsited table, or clear the table, not remove whole table(remove whole table see remove statement). For the unity of grammar, it writied as 'delete TABLE_NAME' instead of 'delete from TABLE_NAME';
>Now you removed the row where AppleCount = 3 and AppleName = Red Fuji;
>Where statement is not required, commend without where statement means clear all elements of the table.

## remove an exsited table:

__remove TABLE_NAME;__

* e.g.
>_remove Apple;__
>You have removed whole table named Apple.

## select data from some tables:

__select * from Apple where CONDITIONS;__
__select <COLUMNS_NAMES> from Apple where CONDITIONS;__

* e.g.
>_select * from Apple;_
>_select <AppleColor, AppleCount> from Apple where AppleCount = 3;_
>Now you got data of Apple as you want to;
>Where statement is not required.

## where statement:
### and / or

>#### __and__
>__CONDITIONS_1 and CONDITIONS_2__
>
>>* e.g.
>>
>>_AppleCount = 1 and AppleColor = red and/or ..._
>>
>>'and' sub statement return the result meet __CONDITIONS_1 and CONDITIONS_2__ simultaneously;
>
>#### __or__
>__CONDITIONS_1 or CONDITIONS_2__
>
>>* e.g.
>>
>>_AppleCount = 1 or AppleColor = red and/or ..._
>>
>>'or' sub statement return the result meet __CONDITIONS_1 or CONDITIONS_2__;
>
>_The 'and' sub statement and 'or' sub statement are on the same grammatical levels in where statement, but 'and' sub statement has a higher priority than 'or''s. Kernel would  process all 'and' statements first and then process the 'or's later, if commend designed not follow this order, please use brackets () to declare the right order, as we recommend already._

### logical operators:  =  /  ==  /  >  /  <  /  >=  /  <=  /  !=

>#### __=  /  ==  /  !=__
>
>>* e.g.
>>
>>_AppleCount = 1_
>>
>>_AppleCount != 1_
>>
>>'=' and '==' are same for liederDB, check whether operating objects are equal;
>>
>>'!=' checks whether operating objects are not equal;
>>'=', '==' and '!=' can use for all types of objects;
>
>#### __>  /  <  /  >=  /  <=__
>
>>* e.g.
>>
>>_AppleCount > 1_
>>
>>_AppleCount <= 1_
>>
>>The role of these symbols is the same as their meaning in mathematics;
>>However, it should be noted that these symbols can only be used when both sides are all numbers, otherwise the kernel will report an error.
