## The purpose of this book

This book demonstrates some key ideas in the interpretation and compilation of programming languages. It is a work in progress: chapters will be added showing how to implement a small Forth, a Lisp, a BASIC, a Z80 emulator, and a compiler targeting the emulator.

It is supposed that the readers of this books will have programmed in at least one programming language, and that they know what a programming 

## Pipefish

The implementation of the various programs is in Pipefish, which can be written like runnable pseudocode, and which can therefore be read by people who have never used any Pipefish. Any aspects of the syntax and/or semantics that need explaining will be pointed out as we go along, with links to the main Pipefish documentation, and will pretty much be covered before we've finished writing our first parser, because among its other merits Pipefish is also very small.

The code is runnable in your browser, because what good is "runnable pseudocode" unless you can run it? Here is an example of a Pipefish service with a TUI: you should find that the code is reasonable, and that in the TUI, things like `greet "world"` and `5!` will do what you expect.

Here is more text.