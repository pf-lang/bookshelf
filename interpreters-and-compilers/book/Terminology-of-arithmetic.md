We're going to begin by writing some **calculators**, algorithms which take arithmetic expressions such as `3! + 4 * (5 + 6)` and evaluate them. We will need some vocabulary.

We know, informally, what it is to **evaluate** `3! + 4 * (5 + 6)`. It has a *meaning*, in this case `50`, and we want to find it out from the original expression.

`3`, `4`, `5`, `6` and `50` are all **values** in our little calculator languages, the things that it's *about*, the data that it manipulates.

Things such as `!` and `+` and `*` are **operators**. Each of them takes in one or more values and produces a value. `3!` *means* `6`; `5 + 6` *means* `11`.

The number of values required for an operator to make sense is called its **arity**. So `+` has arity 2, but `!` has arity 1. The values operated on by an operator are called its **operands**.

`(` and `)` are neither operators nor operands: they are **symbols**, or **punctuation**.