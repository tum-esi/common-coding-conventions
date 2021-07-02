## Additional Implementation Rules

[Read base rules.](../README.md#user-content-implementation)



### Prefer early (compile-time) checking over late (run-time) checking

If possible, use all of the following mechanisms: 
 1. See the compiler as your friend and care for its warnings. The goal is not to write code that compiles but code that is correct (and readable). 
 2. Use a linter. A linter will check your code while you type and provides the earliest feedback. 
 3. Use static typing with many individual types to detect type mismatches early. 
 4. Use static asserts to detect unintended changes to your code. 
 5. Use exceptions with meaningful trace-output as your last line of defense. Consider any OS-Error(e.g. `segfault`) or direct microcontroller-reset as the worst-case and as an indication that your workflow – not only your code – is flawed.



### Code simple, not smart (KISS) and only what you need (YAGNI)

Keep it simple and stupid (KISS): Write straightforward code to achieve
your goal. If you use a compiler, do not try to outsmart it. Compilers
are really sophisticated and can optimize simple code much better than
you.

You Ain't Gonna Need It (YAGNI): Don't code out every little detail that
you can possibly think of. Instead, implement only what is absolutely
necessary but be open for extensions.


### Structure Files into 1. Imports, 2. Constants, 3. Publics, 4. Privates

Structure each code file into parts: 1. imports/includes, 2. lobal constants, 3.
public classes/functions, 4. private classes/functions, and optional 5. direct
instructions in the `main` file. Keep these parts in order and
separated, e.g. do not include files or define globals within a function
declaration. Provide comment headings for these parts such that it easy
to identify them when scrolling through the file.


### Subprograms should either handle states or calculate results

Most languages do not distinguish between procedures and functions but
it is useful. Procedures modify states and may return a value. Pure
functions are stateless and always return a value (or throw an exception
otherwise). At best, a function should only work with the input
variables to make clear on which data it depends. If your subprogram
does change a state and returns a result, make sure to name it as a
procedure (see [3.1](#name:subs){reference-type="ref"
reference="name:subs"}).


### Sort conditions (<) and cases (expected first)

Conditional statements should be written in the form `(3 < x)` instead
of `(x > 3)` even if you think "x larger 3". For most cultures, numbers
increase from left to right and thus it is easier to understand,
especially when you add an upper bound: `(3 < x) && (x < 7)`. Handle the
nominal or expected case first and avoid negations, e.g. use
`if hasElement()` instead of `if not isEmpty()`.


### Return often and soon, if errors ascend, but valid result, just once at the end.

If an input is invalid or if any other error occurs, immediately return
to avoid unnecessary code execution and nested errors. However, valid
results should be returned only at the very end of a function body. By
having a single success exit, it is easier to verify data validity.
Furthermore, fail immediately and loudly. For any severe exception, your
program should immediately crash and output the cause.



### Use what you define and avoid unreachable/dead code.

There should be no unused declarations of variables, arguments,
functions, or classes. Furthermore, avoid *unreachable code* (e.g. after
`return`) and *dead code*, which has no effect (e.g. is redundant).
