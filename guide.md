# F# Primer in 30 minutes!
The aim of this primer is to, within half an hour, introduce you to some of the core features
of F# and exploratory programming:

* The REPL
* Values
* Functions
* Records
* Pipes

## Prerequisites (5-10 minutes)

* .NET Core 2.0+
* VS Code code editor
* Ionide F# extension for VS Code

## The REPL (5 minutes)
The Read Evaluate Print Loop (REPL) in F#, also known as F# Interactive (FSI), is a way to
experiment with F# code and data within the overhead of a full project. You can think of this
as similar to the immediate window if you come from C#, or LINQPad, or Management Studio if you
come from a SQL background.

1. In VS Code, in this folder create a new file with the extension `.fsx` e.g. `scratchpad.fsx`.

> **Tip**: There is no need for a project or solution file when working with F# scripts.

2. In the file, enter the text `"Hello, world"` and hit `ALT + ENTER` to "send" this to the REPL.
3. Observe the text in the REPL: `val it : string = "Hello, world"`. In other words, F# has
identified this as a valid string.
4. Try the same for integers or simple expressions e.g. `1 + 5` or `"Hello" + " world"`

## Values (5 minutes)
You can also create *values* in REPL and assign them to immutable *symbols* which you can reuse
later on.

1. Enter the text `let name = "Fred"` and send it to the REPL.
2. Notice that Ionide decorates the `name` symbol with the word "string", showing you that F#
has correctly inferred the type of the `name` symbol.
3. You can select just the symbol `name` and send that to the REPL to have F# evaluate the value for
you.
4. Now enter on a new line `let town = "Frankfurt"`, and send this to the REPL.
5. Finally, combine the two together: `let details = name + " comes from " + town`

## Functions (5 minutes)
You can create functions that take some arguments and return a value. You create a function using the syntax:

```fsharp
let functionName (arg1:Type) (arg2:Type) : ReturnType =
    expression...
    expression...
    expression // return value of function
```

1. Create a function `greet` that takes in a `forename` and `surname` and returns the text "Hello, forename surname!"
2. Test the function in the REPL with some example inputs.
3. Bind the return value for a call to the function to a symbol, `greeting`.

> **Tip**: You can usually omit the `Type` and `ReturnType` and let F# "figure out the types" for you.

> **Tip**: F# also lets you define and call functions in "tupled" form e.g.
> ```fsharp
> let functionname = (arg1:Type, arg2: Type) : ReturnType = ...
> ```
> This is typically used when calling BCL functions.

You can have multiple lines in a function, and can create symbols within a function.

4. Enhance the function to capitalise the forename and surname before creating the output text.

## Records (5 minutes)
Records act as simple DTOs in F#. They are immutable by default.

1. Declare a record, `Person`, as follows:

```fsharp
type Person = { Forename : string; Surname : string; Age : int }
```

2. Create a function `makePerson` that takes in a forename and surname, capitalises their name,
and creates a Person with age hardcoded to 21. You can create a record as follows:

```fsharp
{ Forename = "..."; Surname = "..."; Age = 99 }
```

> Notice that you don't need to specify the Person type anywhere; the compiler will correctly 
infer this.

3. Enhance the function to use the `System.Random` type to randomly pick an age between 18 and 30.
You can call the `Next()` method on a `Random` object to generate a random number within a range.

4. Bind the result to a symbol, `thePerson`.

> **Tip**: You can access fields on a record using dot notation, just like in other languages like
C# etc.

## Pipes (5-10 minutes)
You can "pipe" arbitrary functions together to make a "pipeline" of functions.

1. Create a function, `add`, that can add two numbers together.
2. Create a function, `multiplyBy`, that can multiply two numbers together.
3. Create a call chain for the following equation using the functions you defined: `1 + 10 * 2`.

Your code will look something like this:
```fsharp
multiplyBy 2 (add 1 10)
```

4. Now replace the code using the `|>` operator:

```fsharp
add 1 10 |> multiplyBy 2
```
> **Tip**: The pipeline operator takes the "right-most" argument and "flips" it over to the left of 
the pipe.

3. Create a call chain for the following equation using the functions you defined.

`1 + 10 + 20 * 3 + 5`

It should look like this:

```fsharp
add 1 10 |> add 20 |> multiplyBy // etc.
```