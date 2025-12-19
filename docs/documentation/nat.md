# nat

The `nat` type represents natural numbers in Katon.

It is a refinement of `int` used to express values that are known to be non-negative. `nat` is commonly used for array indices, sizes, counters, and numeric invariants where negativity is invalid by definition.

## Semantics

A `nat` value denotes an element of the mathematical set ℕ.

Formally:

```cpp
nat ≜ { n ∈ ℤ | n ≥ 0 }
```

Semantically, `nat` is a subset of `int` with an additional non-negativity constraint. At the logical level, `nat` values are represented as mathematical integers together with the invariant that their value is greater than or equal to zero.

## Relationship to `int`

`nat` is not a separate numeric domain from `int`.

- Both `int` and `nat` are represented as mathematical integers
- Every `nat` is an `int`
- Not every `int` is a `nat`

The distinction exists to encode semantic intent and to enable additional verification checks.

## Operations

All arithmetic and comparison operations defined on `int` are also defined on `nat`.

| Operator | Meaning          |
| -------- | ---------------- |
| +        | Addition         |
| \-       | Subtraction      |
| \*       | Multiplication   |
| /        | Integer Division |
| unary -  | Negation         |

Operations on `nat` values produce results of type `int`. Assigning the result back to a `nat` variable requires proving that the result is non-negative.

```go
let x: nat = 5;
let y: int = x - 10;
```

## Assignment and Safety

Assigning a value to a variable of type `nat` requires that the value be provably non-negative.

```go
let n: nat = 10;        // OK
let m: nat = n + 1;     // OK
let k: nat = n - 5;     // Requires proof that n ≥ 5
```

If the verifier cannot prove that the assigned value is greater than or equal to zero, the program is rejected.

## Copy Semantics

Like `int`, `nat` is a **copy** type.

* Reading a `nat` does not consume it

* Assigning or passing a `nat` never invalidates the original value

* `nat` has no ownership, borrowing, or aliasing semantics

```go
let a: nat = 3;
let b: nat = a;
```

## Current Limitations (To Be Fixed)

!!! warning

    Some safety properties of `nat` are not fully enforced yet.

* Certain arithmetic operations may not generate complete non-negativity proofs

* Some assignments rely on conservative SMT checks

* Diagnostic messages for failed `nat` constraints may be incomplete

These limitations are known and will be addressed as Katon’s verification and type systems mature.