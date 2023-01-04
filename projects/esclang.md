an experiment in creating a programming language

# overview
a "what if" project about creating a programming language for [[dotnet]] as a learning experience.

# ideas
a brainstorm of ideas that sound interesting to include or exclude.

## build as code
similar to "infrastructure as code", this is the idea that the metadata necessary to actually build the code is itself code.

using c# as an example, this would mean eliminating the `csproj` project file, and instead providing that metadata as native syntax.

## syntax
syntax might be the least important aspect of creating a new programming language; but certainly there are worthy design choices that would lend to easier readability and ability to refactor.

### no statement termination punctuation
there is some justification for "eliminating the semicolon" above personal preference:
- languages like [[swift]] have done it already
- seems intuitive that readability correlates with having a single statement per line
- increasing code density per line could better accomplished via other abstractions, e.g. a `for` loop with its initialization, condition, and iterator.

# scratchpad
quick notes that might actually be terrible ideas

## syntax: parentheses are always tuples
function call is just a tuple of parameters
