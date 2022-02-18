ideas for a programming language project

-----

for a quicker implementation, imitate scope of QBasic...

compiles to a C# CLI project (or create an interpreter?)
only built-in types
no project, single file as input
no imports
no generics
no polymorphism

-----

basic syntax

```
// variables
x :: 0
y :: true
z :: "hello, world"

// statements
x = x + 1
y = (~y && x == 2) || (y && x == 0)
z.uppercase()

// minimal loop syntax, different semantics using explicit control flow
loop {
	escape if x > 2 // while-loop when at the front, do-while when at the back
}

// minimal conditional syntax, else and else-if via inverse condition
if x == 1 {

}

// procedures
doStuff1 :: () {
    run()
}

doStuff2 :: (a: int) {
    jump(a)
}

doStuff3 :: (a: int, b: int) -> int {
	return a + b
}

```

-----
eliminating semicolons

seems like a challenge to parse statements that can span multiple lines without relying on an end-of-statement token.

currently see two possibilities when seeing an end-of-line token:
* if the current line represents a complete statement, stop
* peek at the next token to see if it can augment the current statement

the first one seems less complicated, so we'll start there

-----
