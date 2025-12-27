# lemma

A `lemma` defines ghost code used solely for verification.

Lemmas have no runtime representation. They do not produce executable behavior; instead, they establish logical facts for the SMT solver.

A lemma may include:

- Postconditions (ensures) describing the property being proven

- An optional body containing proof steps or auxiliary assertions

Unlike `func`, a `lemma` does not return a value to the program—its result is a proven fact that can be used during verification.

```rust
lemma addition_is_commutative(x: int, y: int) {
    ensures x + y == y + x;
    // The body may be empty or contain proof steps
}
```

Once verified, a lemma’s `ensures` clauses become trusted facts that can be reused by the solver, without affecting generated code or runtime behavior.
