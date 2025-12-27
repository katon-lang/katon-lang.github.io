# if/else

## Syntax

```go
if cond {
    // then-block
} else {
    // else-block
}
```

## Semantics

The if / else construct evaluates one of two blocks based on a boolean condition.

- cond must have type Bool
- Exactly one branch is executed
- Both branches are type-checked independently
- Only variables defined in both branches are visible after the if

Katon uses structural merging of branch environments rather than implicit mutation.

## Variable Visibility and Merging

After an if / else:

- A variable is available only if it is defined in both branches
- The variable must have the same type in both branches
- Otherwise, the program is rejected

This ensures deterministic SSA and simplifies verification.

## Example

```go
if b {
    let x = 10;
} else {
    let x = 20;
}

assert x == 10 || x == 20;
```

Valid because `x` is defined in both branches with the same type.

## Invalid Example

```go
if b {
    let x = 10;
} else {
    // x not defined
}

assert x > 0; // error: x not defined in all branches
```

## Type Consistency

If a variable is defined in both branches but with incompatible types, the program is rejected.

```go
if b {
    let x: Int = 1;
} else {
    let x: Bool = true;
}
// error: type mismatch
```

## Borrowing and Updates Across Branches

- Borrowed variables remain read-only within each branch
- Functional updates produce branch-local values
- No mutable aliasing is introduced

```go
let x = [1,2];

if b {
    let y = &x;
} else {
    let y = &x;
}

assert y[0] == 1;
```

Valid: `y` is borrowed consistently in both branches.

## Verification Semantics

- Each branch is verified independently
- Post-condition is checked against the merged environment
- Control flow introduces no implicit side effects
