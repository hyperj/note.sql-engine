# 附录 B（Appendix B）

## 数据类型（Data Types）

Spark SQL and DataFrames support the following data types:

- Numeric types
  - ByteType: Represents 1-byte signed integer numbers. The range of numbers is from -128 to 127.
  - ShortType: Represents 2-byte signed integer numbers. The range of numbers is from -32768 to 32767.
  - IntegerType: Represents 4-byte signed integer numbers. The range of numbers is from -2147483648 to 2147483647.
  - LongType: Represents 8-byte signed integer numbers. The range of numbers is from -9223372036854775808 to 9223372036854775807.
  - FloatType: Represents 4-byte single-precision floating point numbers.
  - DoubleType: Represents 8-byte double-precision floating point numbers.
  - DecimalType: Represents arbitrary-precision signed decimal numbers. Backed internally by java.math.BigDecimal. A BigDecimal consists of an arbitrary precision integer unscaled value and a 32-bit integer scale.
- String type
  - StringType: Represents character string values.
- Binary type
  - BinaryType: Represents byte sequence values.
- Boolean type
  - BooleanType: Represents boolean values.
- Datetime type
  - TimestampType: Represents values comprising values of fields year, month, day, hour, minute, and second.
  - DateType: Represents values comprising values of fields year, month, day.
- Complex types
  - ArrayType(elementType, containsNull): Represents values comprising a sequence of elements with the type of elementType. containsNull is used to indicate if elements in a ArrayType value can have null values.
  - MapType(keyType, valueType, valueContainsNull): Represents values comprising a set of key-value pairs. The data type of keys are described by keyType and the data type of values are described by valueType. For a MapType value, keys are not allowed to have null values. valueContainsNull is used to indicate if values of a MapType value can have null values.
  - StructType(fields): Represents values with the structure described by a sequence of StructFields (fields).
    - StructField(name, dataType, nullable): Represents a field in a StructType. The name of a field is indicated by name. The data type of a field is indicated by dataType. nullable is used to indicate if values of this fields can have null values.

## Manual

### DDL (Data Definition Language) 

CREATE/DROP/ALTER/TRUNCATE/SHOW/DESCRIBE

DATABASE/TABLE/COLUMN/VIEW/~~INDEX/MACRO~~/FUNCTION

### DML (Data Manipulation Language) 

LOAD/INSERT/~~UPDATE/DELETE/MERGE~~

~~IMPORT/EXPORT~~

EXPLAIN

### DQL (Data Query Language) 

SELECT

### DCL (Data Control Language)

~~GRANT/REVOKE~~

~~ROLE/PRIVILEGE~~

### DTL (Data Transaction Language)

~~LOCKS/TRANSACTIONS/COMPACTIONS~~

## Functions

### array_distinct

array_distinct(array) - Removes duplicate values from the array.

**Examples:**

```sql
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Since: 2.4.0

### array_except

array_except(array1, array2) - Returns an array of the elements in array1 but not in array2, without duplicates.

**Examples:**

```sql
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Since: 2.4.0

### array_intersect

array_intersect(array1, array2) - Returns an array of the elements in the intersection of array1 and array2, without duplicates.

**Examples:**

```sql
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Since: 2.4.0

### array_join

array_join(array, delimiter[, nullReplacement]) - Concatenates the elements of the given array using the delimiter and an optional string to replace nulls. If no value is set for nullReplacement, any null value is filtered.

**Examples:**

```sql
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Since: 2.4.0

### array_max

array_max(array) - Returns the maximum value in the array. NULL elements are skipped.

**Examples:**

```sql
> SELECT array_max(array(1, 20, null, 3));
 20
```

Since: 2.4.0

### array_min

array_min(array) - Returns the minimum value in the array. NULL elements are skipped.

**Examples:**

```sql
> SELECT array_min(array(1, 20, null, 3));
 1
```

Since: 2.4.0

### array_position

array_position(array, element) - Returns the (1-based) index of the first element of the array as long.

**Examples:**

```sql
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Since: 2.4.0

### array_remove

array_remove(array, element) - Remove all elements that equal to element from array.

**Examples:**

```sql
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Since: 2.4.0

### array_repeat

array_repeat(element, count) - Returns the array containing element count times.

**Examples:**

```sql
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Since: 2.4.0

### array_sort

array_sort(array) - Sorts the input array in ascending order. The elements of the input array must be orderable. Null elements will be placed at the end of the returned array.

**Examples:**

```sql
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Since: 2.4.0

### array_union

array_union(array1, array2) - Returns an array of the elements in the union of array1 and array2, without duplicates.

**Examples:**

```sql
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Since: 2.4.0

### arrays_overlap

arrays_overlap(a1, a2) - Returns true if a1 contains at least a non-null element present also in a2. If the arrays have no common element and they are both non-empty and either of them contains a null element null is returned, false otherwise.

**Examples:**

```sql
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Since: 2.4.0

### arrays_zip

arrays_zip(a1, a2, ...) - Returns a merged array of structs in which the N-th struct contains all N-th values of input arrays.

**Examples:**

```sql
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Since: 2.4.0

### from_json

from_json(jsonStr, schema[, options]) - Returns a struct value with the given jsonStr and schema.

**Examples:**

```sql
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Since: 2.2.0

### to_json

to_json(expr[, options]) - Returns a json string with a given struct value

**Examples:**

```sql
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Since: 2.2.0

## Reference

- [Spark SQL, Built-in Functions](https://spark.apache.org/docs/latest/api/sql/index.html)



