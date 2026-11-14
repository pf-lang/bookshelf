## Stacks and stack machines

There are a number of ways to evaluate such an expression, and we will look at another one here !!!!!!!!!!!!!. But the most common is a "stack machine".

A **stack** is a list of numbers (or other data, but in this case, numbers) which is accessed by adding numbers to one end (conventionally, the right-hand end, or "top") of the stack, and removing them from the same end, so that the last number you put on to the stack must be the first number you take off. This is usually accompanied by the restriction, or the usage, that you can also only *inspect* the number on top of the stack.

Putting a number on top of the stack is called **pushing** it; the opposite is **popping** a number, where we remove it from the top of the stack and (usually) inspect its value and do something with it in the process, rather than merely discarding it.

A **stack machine** is a virtual machine the state of which is a stack.

## A stack machine for RPN arithmetic

So we can evaluate RPN as follows: Look at each token of the code one at a time. If the token is a number, push it onto the stack. If it is an operation of arity *n*, pop *n* numbers from the stack, apply the operation to them, and push the resulting number onto the stack. Continue until we have run out of tokens, at which point there will be one number on the stack, which will be our answer.

You will notice that this will fail if either:

- At any point in the evalutation, we have an operator with arity `n`, and there are fewer than `n` numbers on the stack.
- We have more than one number left on the stack when we get to the end of the tokens.

If you recall our definition of what it means for an RPN expression to be ill-formed, you will see that these two possible errors correspond to the two possible ways an RPN expression can be ill-formed.

## An implementation in Pipefish

Finally, the code:

```pf-ide
def

foo(n int) :
    n
```