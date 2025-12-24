<p align="center">
  <img src="./assets/logo.svg" width="300">
  <br>
  <br>
  <i>A strict, SMT-powered language for state proofs.</i>
</p>

<br>

Katon is a **proof-oriented verification language** designed to answer a single question:

> _Does this state-transforming computation satisfy its specification?_

Katon is not a general-purpose language; it is a proof-assistant designed to be smaller, stricter, and more principled than traditional verification tools.

Katon exists to make reasoning about mutable state _tractable, predictable,
and fully automated_.

## What Makes Katon Different

Katon is built around a small number of non-negotiable ideas:

- **Verification, not execution**  
  Katon programs describe _state transitions_, not runtime behavior.

- **Ownership eliminates aliasing**  
  Rust-style move semantics remove aliasing at the language level,
  dramatically simplifying reasoning.

- **Automation over interaction**  
  All proof obligations are discharged by SMT solvers.
  There are no tactics, scripts, or interactive proofs.

- **Small types, strong guarantees**  
  A minimal type system keeps verification decidable and solver-friendly.

These constraints are not limitations.
They are what make Katon precise.

## A Glimpse of Katon

A Katon `func` specifies how state may change and what must hold afterward:

```go
func update(arr [int]) {
    arr[0] = 99
    ensures arr[0] == 99
    ensures arr[1] == old(arr)[1]
}
```

## What Katon Is Not

Katon intentionally excludes features that increase proof complexity:

- no general recursion

- no heap allocation

- no higher-order functions

- no interactive proving

Every omission is deliberate.
Every omission keeps reasoning simple.
