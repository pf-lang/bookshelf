Let's define some terms.

A **lexer** (and/or **tokenizer**) takes code considered just as a string of characters, and converts it into the next higher unit of structure, the `token`, for example turning the string `"(-42 + 99) * 4!"` into the list `["(", "-", "42", "+", "99", ")", "*", "4", "!"]`.

Normally instead of the tokens being a list of mere bare strings they have **metadata** to say where in the code they came from: in a mature language, this would include such things as the name of the source code file, the line number, and the position in the line. In our first toy implementations we're not going to do this, but in a real language implementation you should tag *all* your artifacts with metadata showing where they come from: you *will* need it.

A **parser** takes this string of tokens and turns it into a data structure that more closely represents the syntactic structure of the code. The most usual form, and the one we will use here, is to turn the expression into an **abstract syntax tree**, or **AST**, which assigns the tokens to nodes of a tree such that the branches of a node are the arguments of an operation. For example, from the tokens `["(", "-", "42", "+", "99", ")", "*", "4", "!"]`, the AST would be:

```
                 *
                / \
               /   \
              +     !
             / \    |
            |   99  4
            -
            |
            42                
```

 Note that the parentheses have disappeared, because the structure of the AST itself represents the correct grouping of operations.

 A **compiler**, starting from this high point of abstraction, turns the AST into something that is more convenient for the computer to actually execute. This may be the machine code of the computer, or it may be **bytecode**, that is, code that mimics the structure of machine code in being a flat list of instructions to be executed sequentially.

By contrast, a **tree-walking interpreter** (or just **tree-walker**) evaluates the code by executing a recursive evaluation function on the AST which you can probably invent for yourself right now if you look at the diagram above for thirty seconds. (If you can't, it will be explained later.)

An **interpreter** generally is something that executes code *other than* machine code. However, some people use the term "interpreter" to mean only a treewalker, and would call something that executes bytecode a **virtual machine** or **VM**.

If I had to explain what makes it a "virtual machine", I would say the distinction between this and a treewalker is that since the treewalker is just a collection of recursive functions calling one another, it never explicitly has to represent *state*, because the intermediate calculations are automatically pushed onto the stack as stack frames at each function call. By contrast, in the virtual machine model of execution, the state of the machine is explicitly represented and is modified by the successive operations until its state represents our final result.