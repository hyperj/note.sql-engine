# 附录B（Appendix B）

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

* [Spark SQL, Built-in Functions](https://spark.apache.org/docs/latest/api/sql/index.html)



