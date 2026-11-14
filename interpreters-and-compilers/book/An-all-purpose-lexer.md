## A lexer for our calculators

We can use the same lexer for all of our calculator implementations.

Its spec is very simple. It will attach no metadata, so its "tokens" will just be a list where the elements are integers or the characters `'+'`, `'-'`, `'*'`, `'/'`, `'^'`, `'~'`, `'!'`, `'('`, or `')'`.

It will throw some sort of error if it tries to lex anything else, such as `"zebra"` or `{99}`. However, recall that a lexer doesn't know anything about whether the code is well-formed besides whether the tokens are well-formed, and so it will (and should) just as happily tokenise `) * (6 7` as `(6 * 7)`.

## The Pipefish implementation

The implementation of the lexer also introduces you to nearly all the features of Pipefish you'll need to know about, and indeed most of the features it has. We'll mention some of the more important points below the code.

For now, note that the single-character type in Pipefish is called `rune`, as in its parent language, Go, and that runes are appended to strings, and elements to lists, using the `&` operator.

```pf-ide
const 

WHITESPACE = set(' ', '\t')
SYMBOLS = set('+', '-', '*', '/', '^', '~', '!', '(', ')')
NUMERALS = set('0', '1', '2', '3', '4', '5', '6', '7', '8', '9') 

def

lex(code string) :
    first lexHead [], code

private

lexHead(tokens list, code string) -> list, string :
    code == "" :
        tokens, ""
    head in WHITESPACE :
        lexHead tokens, tail 
    head in SYMBOLS :
        lexHead tokens & head, tail 
    head in NUMERALS :
        lexHead tokens & number, numberTail
    else :
        error "unexpected rune `'" + string(head) + "'`"
given :    
    head = code[0]
    tail = code[1::len code]
    number, numberTail = lexNumber tokens, code
    
lexNumber(tokens, code) -> int, string :
    int(numString), tail
given :
    numString = slurpNumber(code)
    tail = code[len(numString)::len(code)]

slurpNumber(code) -> string :
    from numString = "" for _::digit = range code :
        digit in NUMERALS :
            numString & digit 
        else :
            break numString 
```

There are three particularly Pipefish-y things about this, in that pretty much all Pipefish code exhibits these features.

- The `given` blocks. In Pipefish, the local variables of a function are declared in the `given` blocks, rather than assigned in the function, and are immutable for the lifetime of the function. 
- The implicit if-then. Because there is no imperative assignment to be performed, the body of a Pipefish function is just a single expression to be evaluated, and so in functions such as `lexHead`, functions can very concisely be defined by parts.
- The `for` loop in `slurpNumber`. The example very nearly speaks for itself, especially if you're familiar with `for` loops in Go, but for a deeper diver, `for` loops in Pipefish are explained in the main documentation here !!!!!!!!, and for the computer-science-inclined, some of the thinking behind them is explained here !!!!!!!!.