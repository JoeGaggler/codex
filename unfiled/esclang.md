ideas for a programming language project

-----

for a faster implementation, imitate scope of QBasic...

compiles to a C# CLI project
only built-in types
no project, single file as input
no imports
no generics

-----

basic syntax

```
// variables
x :: 0
y :: true
z :: "hello, world"

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

importing

```
you :: #import nuget MyCompany.MyPackage

foo :: you.YourClass() // compiled: var foo = new MyCompany.MyPackage.YourClass();
```

-----

mapping to built-in types and members

```
Number   :: #native int
toString :: (#this: Number) -> String #native ToString
```
says:
* `Number` is a type that is actually the native type `int`
* `toString` is a method on `Number` that is actually the native type's `ToString` method
