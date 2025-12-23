---
title: "Katon Foundation I: Hoare Logic"
draft: true 
date: 2025-12-23
authors:
  - ezrantn
---

Katon is a verification-oriented language. It is not designed to be executed, interpreted, or compiled to machine code. Instead, Katon programs are _proved_.

To make this precise, Katon is founded on Hoare logic — a classical framework for reasoning about program correctness using logical assertions.

Hoare logic answers a simple but fundamental question:

> Under what conditions does a program satisfy its specification?

This question is central to Katon’s design.

## Hoare Triples

At the heart of Hoare logic is the Hoare triple:

$$
\{P\} \quad C \quad \{Q\}
$$

It is read as:

> If the precondition P holds before executing program C, then the postcondition Q holds after C finishes.

In Katon, every function denotes exactly one Hoare triple:

$$
\{ requires\} \quad  body \quad \{ ensures\}
$$

A Katon function is verified if its Hoare triple is logically valid.

## Katon Functions as Hoare Triples

Every Katon function corresponds to exactly one Hoare triple.

```go
func f(...) 
  requires P
{
  body
}
  ensures Q
```

A Katon function is correct if its Hoare triple is logically valid.

## Partial Correctness 

Katon adopts the notion of partial correctness from Hoare logic.

This means:

> If the function is called in a state satisfying requires,
> and if it terminates,
> then ensures holds.

Hoare logic separates _correctness_ from _termination_.
This separation keeps the logic simple and compositional.

## What Hoare Logic Does Not Define

Hoare logic intentionally does not define:

- execution order

- runtime behavior

- performance

- machine state

- how values are computed

It only defines **logical relationships between states**.

Katon inherits this philosophy.

## Specifications as First-Class Citizens

In Hoare logic, specifications are not comments — they are mathematical objects.

The program exists to justify the specification.

In Katon:

- `requires` is not a runtime check

- `ensures` is not documentation

- the function body is evidence that the specification holds

## Why Katon Chooses Hoare Logic

Hoare logic gives Katon:

- a small and well-understood foundation

- compositional reasoning

- a clear notion of correctness

- independence from execution models

Most importantly, it lets Katon answer a single, precise question:

> Is this specification logically satisfied by this program?

