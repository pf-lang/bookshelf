I promised you an interpreter for proper arithmetic expressions, but first, for reasons that will become clear, we'll do an RPN calculator.

**RPN** (short for **Reverse Polish Notation**) is a style of notation where we write the operator on the right-hand side of its operands. Instead of `5 + 3`, we write `5 3 +`.

The disadvantage of this is that complicated expressions become harder for humans to read than our traditional notation with infixes and parentheses. It has some advantages, thoug, and one is that we need neither parentheses nor precedence to express our intent without ambiguity: e.g. the infix expressions `(2 + 3) * 4!` and `2 + (3 * 4!)` in RPN are `2 3 + 4 ! *` and `2 3 4 ! * +` respectively.

We will however have to add an operator. In PEMDAS, we can tell the difference between `-` as a prefix and `-` as an infix. In RPN, we can't, we have to know the arity of the operator, and so we will add `~` for negation to our lexer.

An expression such as `1 +` would be **ill-formed**, since `+` requires two operands; similarly `1 2 3 +` would be ill-formed, because after we've performed the addition we still have two numbers `1 5` with nothing to do with them. A **well-formed** expression will use up its operands and operators at the same time, leaving us with just one number on the stack which will be the correct result.

## Evaluating RPN by rewriting

There are a number of ways to evaluate such an expression. One is to look (at random if you like) for any sequence where n numbers are followed by an operator of arity n, e.g. when `!` follows one number or `*` follows two numbers. Then you calculate that bit of the expression and replace it. You continue doing that until you have one number left. 