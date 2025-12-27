# borrowing

## Syntax

```go
let y = &x;
```

## Semantics

Borrowing creates a read-only binding to an existing value.

- `y` is an alias to the current SSA version of `x`
- No mutation is permitted through `y`
- `x` may still be updated or rebound
- `y` remains bound to the original value

Borrowing restricts names, not data.

## Properties

- Read-only
- No reassignment
- No array updates
- No heap or pointer semantics
- No lifetime tracking
- Erased before SMT generation

## Example

```go
let x = [1, 2];
let y = &x;

let x = update(x, 0, 5);

assert y[0] == 1;
assert x[0] == 5;
```

## Forbidden Operations

```go
y = 10;         // error: cannot assign to borrowed variable
y[0] = 10;      // error: cannot update borrowed variable
```

## Notes

- Borrowing does not copy or move the value
- Borrowed bindings never consume their source
- Borrowing introduces no additional SMT variables
