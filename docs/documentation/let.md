# let

Katon encourages **explicit types** in variable declarations.
Providing the type up front allows the resolver and type-checker to reason about variables immediately, without relying on inference.

The `let` statement supports three forms:

- Uninitialized
- Initialized
- Inferred

```rust
let x: int;        // Declared but uninitialized (tracked by the borrow checker)
let y: nat = 10;   // Declared and initialized
```

Uninitialized variables are explicitly tracked by the borrow checker and cannot be used until they are assigned.

## Arrays

Katon only supports **fixed-size arrays**.
The array size is part of the type, enabling the type-checker to detect out-of-bounds access statically—before the SMT solver is invoked.

```rust
let arr: [5; int] = [1, 2, 3, 4, 5];
let empty: [10; nat]; // Uninitialized array of 10 natural numbers
```

Because the size is encoded in the type, array length mismatches and invalid indexing can be rejected early during type checking.
