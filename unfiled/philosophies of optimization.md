# types
* optimization
* non-pessimization
* fake optimization

## optimization
objective measurement, u-ops, memory, etc.
swapping algorithms, O(N squared) vs O(N log N)

hardcore assembly tweaking, cache misses, performance counters

useful, but not common

## non-pessimization
simply not doing the worst thing.

"minimum amount of work you can possibly do, and type that in"
"never do work that doesn't need to get done"

if your code is not non-pessimized, there's no point in doing actual optimization

## fake optimization
non-objective statements that are repeated as facts. 

may only have truth in very specific scenarios.

in any case, avoid doing this.

examples:
* "Arrays are faster than linked lists."
* "DirectWrite has a cache, so you don't need to write one."

# techniques
know your **theoretical maximum performance**, incorporates the hardware or other lowest-level abstraction that you are working with.

bounds that you must know before any optimization

e.g. you might be required to use someone else's code/abstraction.

just because you're dealt a bad hand, you don't have to add to the complexity to add value

## caching
minimize the number of times calling bad code by caching its results

gives a better API for bad back-end code

sometimes even makes sense to put a good cache in front of a bad cache.

"you put caches in front of things that are slow"

## backwards compatibility
do not use "back-compat" or "legacy" as a reason to write bad code. if necessary, create a "legacy mode" that does that so you can write the good code for 99.9999% of users, and allow that one user to opt-in to pessimal code.

## avoid moving data around
if the incoming data can be used as-is outgoing, there should be no need to move it around

using indices into the data instead of copying data out into a separate structure

## practice
look for things to remove in daily programming

# references
* video series: [philosophies of optimization](https://www.youtube.com/watch?v=pgoetgxecw8) 
