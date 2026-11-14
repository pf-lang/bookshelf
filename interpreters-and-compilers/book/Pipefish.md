## Introducing Pipefish

In this book we will be implementing the various algorithms in the Pipefish programming language. Here is a sample of it: you should find it readable, and if you try it out in the TUI you will find that it responds as you would expect to inputs such as `greet "world"` and `5!`.

```pf-ide
def

foo(i int):
    i
```

## Why Pipefish?

Pipefish brings various benefits to a project such as this:

- It comes very close to being "runnable pseudocode".
- It's very small.
- It's designed to be used interactively in a TUI like this.
- It is very easy to peek inside a Pipefish function and see what it's doing.

Here's an example. We've taken our factorial function and added annotations with `\\` to tell it what to log when it reaches a given line. If we leave the body of the logging annotation blank, the service will figure out what it is we want to know, e.g. in line !!!!!! it will log the condition it tested and whether it succeeded. So just adding `\\` to a line you want to peek at will usually tell you everything you want to know.