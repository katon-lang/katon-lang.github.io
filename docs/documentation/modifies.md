# modifies

## Syntax

```go
func f(p1: T1, p2: T2, ...)
    modifies x1, x2, ...
{
    ...
}
```

## Semantics

`modifies` explicitly declares which variables a function is allowed to update.

In Katon, all updates are pure and functional.
`modifies` does not introduce mutation, aliasing, or side effects.

Instead, it specifies which variables may receive fresh SSA versions during function execution.

- Only variables listed in modifies may be reassigned

- Variables not listed are framed and must remain unchanged

- Reassignment always produces a fresh SSA value

- No variable is mutated in place

Formally, for every variable not listed:

```text
x_post = x_pre
```

## Relation to Affine Typing

Affine types already prevent aliasing.
`modifies` addresses a different concern: framing.

It tells the verifier exactly which values may change across a function boundary, allowing precise reasoning without heap havoc or separation logic. Affine typing ensures safety of access; modifies ensures clarity of change.

## Interaction with Update

`modifies` composes naturally with [update](./update.md).

```go
x = update(x, i, v);
```

`update` is pure and referentially transparent. It does not consume or mutate its base. Reassigning the result to x is only legal if x appears in modifies. In verification, this becomes an SMT store over a fresh SSA value.
