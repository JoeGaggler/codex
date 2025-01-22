an experiment in creating a programming language

# overview
a "what if" project about creating a programming language for [[dotnet]] as a learning experience.

# ideas
a brainstorm of ideas that sound interesting to include or exclude.

## build as code
similar to "infrastructure as code", this is the idea that the metadata necessary to actually build the code is itself code.

using c# as an example, this would mean eliminating the `csproj` project file, and instead providing that metadata as native syntax.

extending this idea allows us to write "scripts" that run immediately instead of first outputting an executable.

## syntax
syntax might be the least important aspect of creating a new programming language; but certainly there are worthy design choices that would lend to easier readability and ability to refactor.

### no statement termination punctuation
there is some justification for "eliminating the semicolon" above personal preference:
- languages like [[swift]] have done it already
- seems intuitive that readability correlates with having a single statement per line
- increasing code density per line could better accomplished via other abstractions, e.g. a `for` loop with its initialization, condition, and iterator.

### eliminate parentheses around conditionals
c# keywords such as `if` and `while` require parentheses to avoid ambiguity with single-statement bodies.

# scratchpad
quick notes that might actually be terrible ideas

## single-statement operator
assuming that single-statement bodies are popular and adding braces around them are annoying, then [[#eliminate parentheses around conditionals|avoiding ambiguity]] likely requires an delineating operator, perhaps the arrow: `if condition -> launch()`

# feature parity
method for designing the language by making sure it has essential feature parity with other familiar languages.
## declarations
forget c-like declaration. let's instead be inspired by pascal/odin/jai *or even the english dictionary*:
```
term: definition
```

i anticipate we can generalize every possible declaration with this fundamental syntax.
the left side is always the identifier, and is straight-forward.
the right side is the definition, which will need to be much more complicated.

variable: `foo: int`
with value: `foo: int = 13`

as [odin](https://odin-lang.org/news/declaration-syntax/#syntactic-meaning-of-) shows, this makes implicit type assignments really natural by just omitting the type: `foo := 13`

functions are blocks of code, and while languages like `F#` can successfully avoid braces, i just *really like* braces.
so here's the minimum function declaration: `func := { }`
utterly useless so far, but it already makes sense, and it's expandable.

the next step is to allow for an explicit type.
my current idea is that it looks like a minified function: `func: { } = { blah blah blah }`
again, this still looks pretty useless, but we're getting to the interesting parts

my plan for parameter declarations leans toward [swift closure syntax](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Closure-Expression-Syntax) in that the parameters are *inside* the braces.
this makes sense because typical scope and usage of parameters is often indistinguishable from local variables.
the first issue, then, is to distinguish it from a local, indicating that the value is assigned by the caller.

we do this with angle brackets:
```go
myfunc := {
    myparam: int = <>
}
```

this allows us to specify a default value inside:
```go
myfunc := {
    myparam1 := <>
    myparam2 := <13>
    myparam3 : int = <>
    myparam4 : int = <13>
}
```
this syntax is consistent, but note that `myparam1` cannot be type-inferred from this declaration alone.

let's circle back and show explicit function type declarations. the type can be read as "code block that takes two ints":
```go
myfunc: {int int} = {
```

function with parameters and a return value, use `:` as a separator:
```go
myfunc: {int int : char} = {
```

if there are no parameters we need the initial `:` to distinguish from a parameter:
```go
myfunc: {:char} = {
```

function call does not require parentheses, and parameters just follow without commas:
```go
// myfunc takes 3 ints
myfunc 1 2 3
```

