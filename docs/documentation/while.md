# while

Loops are one of the most challenging constructs to verify.
For this reason, **loop invariants are mandatory** for while `loops` in Katon v0.1.0.

A `while` loop must include one or more `invariant` clauses that describe properties preserved by every iteration. These invariants are used by the verifier to reason about loop correctness and termination.

```rust
while i < arr.length() {
    invariant i >= 0 && i <= 5;
    invariant sum >= 0;

    sum = sum + arr[i];
    i = i + 1;
}
```

In this example, the invariants ensure that the loop index remains within bounds and that `sum` stays non-negative throughout the loop execution.
