## Implementation

Once you have an initial plan for the architecture, you can start
writing the code for classes and subprograms.


#### Code simple, not smart (KISS) and only what you need (YAGNI)

Keep it simple and stupid (KISS): Write straightforward code to achieve
your goal. If you use a compiler, do not try to outsmart it. Compilers
are really sophisticated and can optimize simple code much better than
you.

You Ain't Gonna Need It (YAGNI): Don't code out every little detail that
you can possibly think of. Instead, implement only what is absolutely
necessary but be open for extensions.


#### Don't Repeat Yourself (DRY)

Any piece of data or logic must have a single, unambiguous source. If
you repeat more than 2 statements more than 2 times, write a new
subprogram. At best, any atomic change in program logic should only
affect a single line of code.


#### Keep scopes small and sorted

Define functions and variables in the smallest possible scope and limit
their exposure to external code. Put all declarations at the beginning
of each scope and initialize variables directly at the declaration. Do
not reuse variables in nested scopes or for different purposes.


#### Structure Files into 1. Imports, 2. Constants, 3. Publics, 4. Privates

Structure each code file into parts: 1. imports/includes, 2. lobal constants, 3.
public classes/functions, 4. private classes/functions, and optional 5. direct
instructions in the `main` file. Keep these parts in order and
separated, e.g. do not include files or define globals within a function
declaration. Provide comment headings for these parts such that it easy
to identify them when scrolling through the file.



#### Subprograms should either handle states or calculate results

Most languages do not distinguish between procedures and functions but
it is useful. Procedures modify states and may return a value. Pure
functions are stateless and always return a value (or throw an exception
otherwise). At best, a function should only work with the input
variables to make clear on which data it depends. If your subprogram
does change a state and returns a result, make sure to name it as a
procedure (see [3.1](#name:subs){reference-type="ref"
reference="name:subs"}).


#### Sort arguments and limit them to 0 – 4 per function call.

If you can't avoid output-arguments, place them first. Place mandatory
input arguments second and optional arguments (e.g flags) at the end. If
your argument list grows too long, try to combine related arguments in a
new data structure. For example, instead of passing `x`, `y`, `z`
coordinates individually, use a vector. Call state-changing procedures
on the owning object, e.g. use `report.appendFooter()` instead of
`appendFooter(report)`.

#### Sort conditions (<) and cases (expected first)

Conditional statements should be written in the form `(3 < x)` instead
of `(x > 3)` even if you think "x larger 3". For most cultures, numbers
increase from left to right and thus it is easier to understand,
especially when you add an upper bound: `(3 < x) && (x < 7)`. Handle the
nominal or expected case first and avoid negations, e.g. use
`if hasElement()` instead of `if not isEmpty()`.


#### Return often and soon, if errors ascend, but valid result, just once at the end.

If an input is invalid or if any other error occurs, immediately return
to avoid unnecessary code execution and nested errors. However, valid
results should be returned only at the very end of a function body. By
having a single success exit, it is easier to verify data validity.
Furthermore, fail immediately and loudly. For any severe exception, your
program should immediately crash and output the cause.


#### Express Ideas in Code: Use Domain-Specific Names

Create new types or derive subtypes from primitives to create more
specific names. Especially for physical quantities. Avoid magic numbers
(literal numbers with unclear origin/purpose) but always create
constants with meaningful names. If something must be a positive number,
never use `Int` but `Uint`.


**Bad**
```c
double limit = 13.89;
from_to(int x,  int y,
        int x2, int y2);
if (speed > limit && 
   t.h > 22 && t.h < 6){..}
```

**Better**
```c
MeterPerSecond limit = SPEEDLIMIT_NIGHT;
drive(Point origin, Point dest);
isNight=(T_NIGHT_MIN < t.h && t.h < T_NIGHT_MAX);
isSpeeding=(limit < speed);
if (isSpeeding && isNight){..}
```


#### Do not change the same variable in steps but compose once from parts

Within a function, do not modify the same variable in several steps,
e.g. by summing up an amount using `total += ...` multiple times.
Instead, call functions that return some part of the final value and
then compose the final value of these parts in one instruction at the
end. E.g. `total = partA + partB`.


**Bad**
```c
totalIncome = 0 
// ... long code to get contract
totalIncome += contract.salary  
// ... long code to access taxoffice
totalIncome -= taxoffice[id].tax
```

**Better**
```c
Int totalIncome(employee){      
    salary = getSalary(employee)
    tax    = getTax(employee)   
    return (salary - tax)       
}
```                            


#### Prefer early (compile-time) checking over late (run-time) checking

If possible, use all of the following mechanisms: 
 1. See the compiler as your friend and care for its warnings. The goal is not to write code that compiles but code that is correct (and readable). 
 2. Use a linter. A linter will check your code while you type and provides the earliest feedback. 
 3. Use static typing with many individual types to detect type mismatches early. 
 4. Use static asserts to detect unintended changes to your code. 
 5. Use exceptions with meaningful trace-output as your last line of defense. Consider any OS-Error(e.g. `segfault`) or direct microcontroller-reset as the worst-case and as an indication that your workflow – not only your code – is flawed.


#### Use what you define and avoid unreachable/dead code.

There should be no unused declarations of variables, arguments,
functions, or classes. Furthermore, avoid *unreachable code* (e.g. after
`return`) and *dead code*, which has no effect (e.g. is redundant).
