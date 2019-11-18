# Bit functions

Bit functions work for any pair of types from UInt8, UInt16, UInt32, UInt64, Int8, Int16, Int32, Int64, Float32, or Float64.

The result type is an integer with bits equal to the maximum bits of its arguments. If at least one of the arguments is signed, the result is a signed number. If an argument is a floating-point number, it is cast to Int64.

## bitAnd(a, b)

## bitOr(a, b)

## bitXor(a, b)

## bitNot(a)

## bitShiftLeft(a, b)

## bitShiftRight(a, b)

## bitRotateLeft(a, b)

## bitRotateRight(a, b)

## bitTest {#bittest}

Takes any integer and converts it into binary form, returns the value of a bit at specified position.

**Syntax** 

```sql
SELECT bitTest(number, index)
```

**Parameters**

- `number` – integer number.
- `index` – position of bit. 

**Returned values**

Returns a value of bit at specified position.

Type: `UInt8`.

**Example**

Query:

```sql
SELECT bitTest(43, 1)
```

Result:

```text
┌─bitTest(43, 1)─┐
│              1 │
└────────────────┘
```
Another example:

Query:

```sql
SELECT bitTest(43, 2)
```
Result:

```text
┌─bitTest(43, 2)─┐
│              0 │
└────────────────┘
```

## bitTestAll {#bittestall}

Returns result of [logical conjuction](https://en.wikipedia.org/wiki/Logical_conjunction) (AND operator) of all bits at given positions.

**Syntax** 

```sql
SELECT bitTestAll(number, index1, index2, ...)
```

**Parameters** 

- `number` – integer number.
- `index1` – position of bit. 
- `index2` – position of bit.

**Returned values**

Returns result of logical conjuction.

Type: `UInt8`.

**Example**

Query:

```sql
SELECT bitTestAll(43, 0, 1, 3, 5)
```

Result:

```text
┌─bitTestAll(43, 0, 1, 3, 5)─┐
│                          1 │
└────────────────────────────┘
```

Another example

Query:

```sql
SELECT bitTestAll(43, 0, 1, 3, 5, 2)
```

Result:

```text
┌─bitTestAll(43, 0, 1, 3, 5, 2)─┐
│                             0 │
└───────────────────────────────┘
```

## bitTestAny {#bittestany}

Returns result of [logical disjunction](https://en.wikipedia.org/wiki/Logical_disjunction) (OR operator) of all bits at given positions.

**Syntax** 

```sql
SELECT bitTestAny(number, index1, index2, ...)
```

**Parameters** 

- `number` – integer number.
- `index1` – position of bit. 
- `index2` – position of bit.

**Returned values**

Returns result of logical disjuction.

Type: `UInt8`.

**Example**

Query:

```sql
SELECT bitTestAny(43, 0, 2)
```

Result:

```text
┌─bitTestAny(43, 0, 2)─┐
│                    1 │
└──────────────────────┘
```

Another example:

Query:

```sql
SELECT bitTestAny(43, 4, 2)
```

Result:

```text
┌─bitTestAny(43, 4, 2)─┐
│                    0 │
└──────────────────────┘
```



[Original article](https://clickhouse.yandex/docs/en/query_language/functions/bit_functions/) <!--hide-->
