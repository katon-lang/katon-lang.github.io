# update

## Syntax

```go
let x2 = update(x, i, v);
```

## Semantics

`update` performs a pure functional update on an aggregate value (currently arrays).

- Returns a new value
- Does not mutate `x`
- `x` remains usable after the update
- Produces a fresh SSA value
- Referentially transparent

Formally, for arrays:

```go
x2 = store(x, i, v)
```

## Properties

- No aliasing
- No side effects
- Safe under verification
- Composes naturally with SSA
- Deterministic and total (subject to bounds checking)

## Example

```go
let x = [1, 2, 3];
let x2 = update(x, 0, 10);

assert x[0] == 1;
assert x2[0] == 10;
```

## Notes

- `update` does not consume `x`
- Index bounds are statically checked when possible
- Dynamic bounds are discharged to the SMT solver
