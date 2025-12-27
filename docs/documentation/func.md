# func

A `func` defines a **callable, executable unit** that can returns a value.

Functions may have side effects (for example, once mutability is introduced), but their behavior is **specified and constrained by contracts**. Every `func` must be verified to satisfy its specification.

Each function can include:

- Preconditions (`requires`) that must hold at call time

- Postconditions (`ensures`) that must hold on return

The return value is referred to as result inside postconditions.

```rust
func add_one(x: int) -> int {
    requires x < 100;
    ensures result == x + 1;

    return x + 1;
}
```

In this example, the function is only valid for inputs less than `100`, and the verifier guarantees that the returned value is exactly `x + 1`. If verification succeeds, the function is emitted as executable code.
