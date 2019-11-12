# Conditional functions

## if {#if}

`if` - is a [ternary operation](https://en.wikipedia.org/wiki/Ternary_operation). 
Evaluates condition `cond` and executes `then` expression if condition is met. Executes `else` otherwise.

**Syntax** 

```sql
SELECT if(cond, then, else)
```

**Parameters** (Optional)

- `cond` – The condition for evaluation. [UInt8](https://clickhouse.yandex/docs/ru/data_types/int_uint/).
- `then` - The expression executed if condition is met. Any [data type](https://clickhouse.yandex/docs/en/data_types/).
- `else` - The expression executed if condition is not met. Any [data type](https://clickhouse.yandex/docs/en/data_types/).

**Returned values**

The function executes `then` or `else` expression and returns its result, depending on the condition `cond`.
Expressions `then` and `else` can be `NULL`, any expressions or have an explicit values.
Returns any [data type](https://clickhouse.yandex/docs/en/data_types/).

**Example**

Query:

```sql
SELECT IF(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)') > 0, plus(2, 2), null)
```

Result:

```text
┌─IF(greater(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)'), 0), plus(2, 2), NULL)─┐
│                                                                          4 │
└────────────────────────────────────────────────────────────────────────────┘
```

Query:

```sql
SELECT IF(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)') > 1, plus(2, 2), null)
```
Result:

```text
┌─IF(greater(CAST('a', 'Enum8(\'a\' = 1, \'b\' = 2)'), 1), plus(2, 2), NULL)─┐
│                                                                       ᴺᵁᴸᴸ │
└────────────────────────────────────────────────────────────────────────────┘
```

## multiIf

Allows you to write the [CASE](../operators.md#operator_case) operator more compactly in the query.

```sql
multiIf(cond_1, then_1, cond_2, then_2...else)
```

**Parameters:**

- `cond_N` — The condition for the function to return `then_N`.
- `then_N` — The result of the function when executed.
- `else` — The result of the function if none of the conditions is met.

The function accepts `2N+1` parameters.

**Returned values**

The function returns one of the values `then_N` or `else`, depending on the conditions `cond_N`.

**Example**

Take the table

```text
┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │    3 │
└───┴──────┘
```

Run the query `SELECT multiIf(isNull(y) x, y < 3, y, NULL) FROM t_null`. Result:

```text
┌─multiIf(isNull(y), x, less(y, 3), y, NULL)─┐
│                                          1 │
│                                       ᴺᵁᴸᴸ │
└────────────────────────────────────────────┘
```

[Original article](https://clickhouse.yandex/docs/en/query_language/functions/conditional_functions/) <!--hide-->
