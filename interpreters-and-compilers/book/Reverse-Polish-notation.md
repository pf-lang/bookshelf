## RPN defined

**RPN** (short for **Reverse Polish Notation**) is a style of notation where we write the operator on the right-hand side of its operands. Instead of `5 + 3`, we write `5 3 +`.

The disadvantage of this is that complicated expressions become harder for humans to read than our traditional notation with infixes and parentheses. It has some advantages, though, and one is that we need neither parentheses nor precedence to express our intent without ambiguity: e.g. the infix expressions `(2 + 3) * 4!` and `2 + (3 * 4!)` in RPN are `2 3 + 4 ! *` and `2 3 4 ! * +` respectively.

We will however have to add an operator. In PEMDAS, we can tell the difference between `-` as a prefix and `-` as an infix. In RPN, we can't, because we have to know the arity of the operator to evaluate it, and so in our lexer we supplied an operator `~` to represent an operator of arity `n` that negates a number.

## Well-formed expressions

An expression such as `1 +` would be **ill-formed**, since `+` requires two operands. If we tried to evaluate it, this would be an error known as a **stack underflow**, for reasons which will become clear on the next page.

Similarly `1 2 3 +` would be ill-formed, because after we've performed the addition we still have two numbers `1 5` with nothing to do with them.

A **well-formed** expression will use up its operands and operators at the same time, leaving us with just one number which will be the correct result.