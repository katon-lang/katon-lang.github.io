# Semantics of Katon

This page describes the **formal semantic model** of the Katon Verification Language.

Katon does not define execution semantics in the traditional sense.
Instead, it defines a _verification semantics_: how programs are translated into logical formulas and checked by an SMT solver.

## Verification-Oriented Semantics

A Katon program is not executed.
It is **compiled into verification conditions (VCs)** that must be proven valid.

Semantics answer the question:

> _Under what logical conditions is this specification satisfied?_

There is no runtime, no machine state, and no observable behavior.
Only logical truth.

## State as Logical Variables

Katon models program state as a collection of **logical variables**.

- Each variable represents a value at a specific program point
- State changes create _new_ logical variables
- Old values are never mutated or destroyed

State is therefore _persistent_ and _immutable_ at the semantic level.

## Static Single Assignment (SSA)

All Katon programs are translated into **Static Single Assignment (SSA)** form.

In SSA:

- Every variable is assigned exactly once
- Each assignment introduces a fresh version of that variable

Example:

```go
x = 1
x = x + 1
```

Is translated conceptually into:

```text
x_0 = 1
x_1 = x_0 + 1
```

This eliminates implicit temporal reasoning.
All data dependencies are explicit in the logic.

## Mutation as Versioning

What appears as mutation in Katon syntax is **version creation** semantically.

For arrays:

```katon
arr[0] = 99
```

Is translated into:

```text
arr_1 = store(arr_0, 0, 99)
```

Where:

- `arr_0` is the array before the update
- `arr_1` is the array after the update
- `store` is the SMT array update function

No array is ever modified in-place.

## The Meaning of `old`

The expression `old(e)` refers to the value of `e` in the **pre-state** of a `func`.

Semantically:

- All parameters and mutable variables are given an initial version
- `old(x)` is resolved to that initial version (`x_0`)

Example:

```katon
ensures arr[1] == old(arr)[1]
```

Is translated into:

```text
select(arr_final, 1) == select(arr_0, 1)
```

Because SSA versions are explicit, `old` is unambiguous and requires no temporal logic.

## Verification Conditions

Katon doesn't "run" your code to see if it works. Instead, it bundles your entire function—the requirements, the logic, and the goals—into a single massive logical question called a Verification Condition (VC).

The question looks like this:

$$Preconditions ⟹ Postconditions$$

Katon hands this formula to an SMT solver. The solver doesn't look for a way to execute the code; it looks for a counter-example. It asks: _"Is there any possible set of numbers where the '`requires`' are true, but the '`ensures`' are false?"_ If the solver finds even one such case (like an integer overflow or a boundary error), the program is **Invalid**.

- If the solver proves no such case can ever exist, the program is **Verified**.

## Quantifier-Free SMT Fragment

Katon targets a restricted SMT logic:

- **QF_AUFNIA** (quantifier-free arrays, uninterpreted functions, and nonlinear integer arithmetic)

Design consequences:

- No user-defined quantifiers
- No higher-order reasoning
- No solver hints or tactics

This restriction keeps solver behavior predictable and scalable.

## Totality and Definedness

All Katon functions are **total** by construction.

- Division by zero
- Out-of-bounds access
- Invalid arithmetic

Must be ruled out by preconditions or proven impossible.

If definedness cannot be proven automatically, verification fails.

## Absence of Control-Flow Semantics

Katon does not model:

- loops as execution constructs
- recursion as computation
- branching as control flow

Instead:

- conditionals are translated into logical implications
- invariants are treated as assumptions

There is no notion of step-by-step execution.

## Soundness Boundary

Katon is sound **relative to its SMT backend**.

That is:

- If verification succeeds, the specification holds in the SMT model
- If the solver is unsound, Katon inherits that unsoundness

Katon intentionally avoids features that would widen this boundary.

## Summary

Katon is not a language for telling a computer what to do. It is a language for telling a solver what must be true. By stripping away the concepts of registers, clocks, and memory, Katon turns programming into a pure exercise in geometry and truth.
