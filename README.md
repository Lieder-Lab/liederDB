# liederDB_liederImitateSQL
updating...

Optimized MySQL, support middle layer storage, more modular syntax and more optimized operation speed.
All elements save as String in kernel, so default element type is String.

# Grammar regulation(Different from MySQL):
  <ARRAY_NAME> means <1st, 2nd, 3rd, ...>


# Create new table with initialize columns:

  create TABLE_NAME set <COLUMNS_NAME> [type <COLUMNS_TYPE>];
  
  $e.g
  create Apple set <AppleName, AppleCount, AppleColor>;
  You would create a table named Apple which has 3 columns named separately AppleName, AppleCount and AppleColor.
  [type <COLUMNS_TYPE>] means you can assign every column with corresponding types, but should note that the length of COLUMNS_TYPE array should be equal as COLUMNS_NAME's length.
