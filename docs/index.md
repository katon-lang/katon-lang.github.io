<<<<<<< Updated upstream
# Katon IVL

_A small, automated verification language for reasoning about state changes._

## Overview

Katon is an **intermediate verification language** designed to answer a single question:

> _Does this state-transforming computation satisfy its specification?_

It is not a general-purpose programming language.
It is a **proof-assistant theorem language**, in the spirit of Dafny,
but deliberately **smaller, stricter, and more principled**.

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
=======
# Katon Verification Language
*A small, automated verification language for reasoning about state changes.*

## Overview

Katon is a **verification-first language** designed to answer a single question:

> *Does this state-transforming computation satisfy its specification?*

It is not a general-purpose programming language.
It is a **proof-assistant theorem language**, in the spirit of Dafny,
but deliberately **smaller, stricter, and more principled**.

Katon exists to make reasoning about mutable state *tractable, predictable,
and fully automated*.

## What Makes Katon Different

Katon is built around a small number of non-negotiable ideas:

* **Verification, not execution**  
  Katon programs describe *state transitions*, not runtime behavior.

* **Ownership eliminates aliasing**  
  Rust-style move semantics remove aliasing at the language level,
  dramatically simplifying reasoning.

* **Automation over interaction**  
  All proof obligations are discharged by SMT solvers.
  There are no tactics, scripts, or interactive proofs.

* **Small types, strong guarantees**  
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

* no general recursion

* no heap allocation

* no higher-order functions

* no interactive proving

Every omission is deliberate.
Every omission keeps reasoning simple.
>>>>>>> Stashed changes
