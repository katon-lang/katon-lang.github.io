# int

The `int` type represents mathematical integers in Katon. It is the most fundamental value type and is used for arithmetic, indexing, counters, and reasoning about numeric state changes.

Unlike machine integers in systems languages, `int` in Katon is unbounded and purely logical: it models integers as they exist in mathematics, not as fixed‑width hardware values.

## Semantics

An `int` value denotes an element of the mathematical set ℤ.

Formally

```cpp
int ≜ ℤ
```

All operations on `int` are interpreted as exact mathematical operations. There is no overflow, underflow, or wrapping behavior.

Katon deliberately uses the same `int` type for both:

- executable expressions, and
- logical specifications (preconditions, postconditions, invariants).

There is no distinction between “runtime integers” and “specification integers”.

## Basic Usage

```go
let x: int = 10;
let y: int = x + 5;
let z: int = -y;
```

Assignments conceptually create a new logical value; `int` values themselves are immutable.

## Arithmetic Operations

The following arithmetic operations are defined on `int`:

| Operator | Meaning          |
| -------- | ---------------- |
| +        | Addition         |
| \-       | Subtraction      |
| \*       | Multiplication   |
| /        | Integer Division |
| unary -  | Negation         |

Example:

```go
let a: int = 7;
let b: int = 3;

let sum  = a + b;   // 10
let diff = a - b;   // 4
let prod = a * b;   // 21
```

## Copy Semantics

`int` is a **copy** type.

- Reading an `int` does not consume it
- Assigning or passing an `int` never invalidates the original value
- There is no ownership transfer, borrowing, or aliasing

```go
let a: int = 5;
let b: int = a;   // always allowed
```

## Current Limitations (To Be Fixed)

!!! warning

    Some safety properties of `int` are not fully enforced yet.

- Division by zero is not consistently rejected at verification time
- Some arithmetic safety checks are still being formalized
- Error messages related to numeric misuse may be incomplete

These limitations are known and temporary.
They will be addressed as Katon’s verification condition generation and type system mature.
