![header-logo](img/tum-ei-esi-header.png)


&nbsp;
# Software Design Guide

The goal of this guide is to be concise, universal, and remarkable. It covers 6 topics:

  1. [Architecture](#user-content-architecture), 
  2. [Implementation](#user-content-implementation), 
  3. [Naming](#user-content-naming), 
  4. [Code Layout](#user-content-code-layout), 
  5. [Documentation](#user-content-documentation), and 
  6. [Languages](#user-content-languages). 

To follow this guide, you should already know basic programming rules, such as
writing loops and meaningful functions instead of copy pasting
instructions. 
In this Readme, we will shortly summarize the most important rules for every topic. More rules and details can be found if you follow the links at each heading. 

While it might be difficult to recall all rules later, try to remember the underlying philosophy of this guide:

> Keep it simple and solid, let the toolchain be smart,  
> code correctness is the duty and readability the art.


&nbsp;
## Clarifications First

#### Be Consistent with the Existent

"Consistency with this guide is important. Consistency within a project
is more important. Consistency within one module or function is the most
important" [1].



#### Break rules if it enhances clarity. 

Do not blindly follow this guide but think for yourself. The goal of
software development is keeping the code complexity low. Period. None of
the fancy patterns matters if the code becomes impossible to maintain.



#### Terminology

To be universal, we group several concepts under these broad
identifiers:


 * **Scope**       ={Module, File Namespace, Subprogram}                
 * **Subprogram**  ={Procedure, Function, Method}
 * **Type**        ={Primitive, Collection, Struct, Class, ...}   
 * **Collection**  ={Array, List, Tuple, Dict, Map, ...}




&nbsp;
## [Architecture](chapter/1_architecture.md)

To manage complexity, divide your software into smaller parts (scopes)
such as modules, classes, and subprograms. Where to separate and where
to connect scopes is the art of good architecture.


#### Aim for coherent abstraction levels

Each scope should reflect a single coherent level of abstraction that
corresponds to its hierarchy level. In your UML, abstraction should
decrease from top to bottom. In your code, the deeper you are in a call
tree, the more specific your instructions can be. Avoid state variables
at high abstraction levels.


**Bad**
```python
engine.start()
nStartUps += 1
if fuelTank.isEmpty():
  fuelGaugeUI.setRedLED()
```

**Better**
```python
engine.start()
engine.runTest():
warnings = engine.warnings()
dashboard.show( warnings )
```



*Mixing abstraction levels creates confusion and introduces unnecessary
dependencies.*


#### Aim for low coupling between classes

You may have many classes but each class should communicate with as few
others as possible. If any two classes communicate at all, they should
exchange as little information as possible.

Data classes should only be changed by a single supervisor class or
passed on in a strict [Chain of Responsibility](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern).
If two independent classes write to the same data class, the risk for
conflicts increases.





&nbsp;
## [Implementation](chapter/2_implementation.md)

Once you have an initial plan for the architecture, you can start
writing the code for classes and subprograms.


#### Don't Repeat Yourself (DRY)

Any piece of data or logic must have a single, unambiguous source. If
you repeat more than 2 statements more than 2 times, write a new
subprogram. At best, any atomic change in program logic should only
affect a single line of code.



#### Keep all scopes (File/Class/Function) small and sorted

Define functions and variables in the smallest possible scope and limit
their exposure to external code. Put all declarations at the beginning
of each scope and initialize variables directly at the declaration. Do
not reuse variables in nested scopes or for different purposes.


#### Sort arguments and limit them to 0 – 4 per function call.

If your argument list grows too long, try to combine related arguments in a
new data structure. For example, instead of passing `x`, `y`, `z`
coordinates individually, use a vector. 



#### Express Ideas in Code: Use Domain-Specific Names

Avoid magic numbers (literal numbers with unclear origin/purpose) 
but always create constants with meaningful names. 
Create new types or derive subtypes from primitives to create more
specific names. Especially for physical quantities. 


**Bad**
```c
double limit = 13.89;        // unit not clear
from_to(int x,  int y,
        int x2, int y2);

if (speed > limit && 
   t.h > 22 && t.h < 6){..}  // 22 and 6 are magic numbers
```

**Better**
```c
MeterPerSecond limit = SPEED_LIMIT_NIGHT;
drive(Point origin, Point dest);

isNight    = (T_NIGHT_MIN < t.h && t.h < T_NIGHT_MAX);
isSpeeding = (limit < speed);
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




&nbsp;
## [Naming](chapter/3_naming.md)
Code should communicate behavior to other humans with lower complexity than the behavior it inherits. Abstracting with meaningful names is most important for readability.


#### Subprograms (=Procedure/Function)
Procedures *may* return values, functions always return a value. Methods are subprograms of a class.
 * procedure names should start with a verb. e.g. `syncViews()`, `list.addItem(x)`.
 * function names should describe the result and, if suitable, its type. e.g. `time_ms(), sin(x)`
 * class methods should not repeat or include the name of the class. Define `Line.length()`, not `Line.getLineLength()`

*Single noun subprograms must be pure functions! Never let e.g. `x.length()` change a state.*


#### Types (=Class/Struct/Subtypes)
 * type names should be capitalized nouns. E.g. `Integer`, `Date`, `Line2D`
 * Enums/Structs are types and named as types without a special prefix/suffix.
 * Interface names should start with a capital `I` and can also be adjectives. E.g. `IObservable`


#### Variables
 * variables with a large scope *should* have long names, variables with a small scope *can* have short names.
 * collections (set, array, dict) should have a plural name. E.g. `cars`, `indices`
 * the prefix `n` or `num` should be used for names representing the total number of objects in a collection. E.g. `nCars`
 * boolean variables should start with a `is/has/can/does` prefix (e.g. `isEmpty`, `doesUseIO`).
 * write constant names in capitals. E.g `CFG_TEMPERATURE_MAX = 80.0`
 * prefix global and static variables with `g_` and `s_`





&nbsp;
## [Code Layout](chapter/4_layout.md)
A clear and consistent visual appearance of your code improves readability and readability helps to understand the code.

 * Existing Project: Stick to the existing recommendation and tools.
 * New Project: Use an automatic code layouter. Examples:

| Language   | Tool   |   
|:-----------|--------|
| C          | [uncrustify](http://uncrustify.sourceforge.net/) |
| Python     | [black](https://pypi.org/project/black/) |
| C++        | [clang-format](http://clang.llvm.org/docs/ClangFormat.html) |
| JavaScript | [prettier.io](https://prettier.io/) |




&nbsp;
## [Documentation](chapter/5_documentation.md)
English is the language of programming, so documentation should also be in English.


#### Comments
Comments that contradict the code are worse than no comments. Change comments when code changes.
Comment only what the code cannot say, that is *why* you did it, maybe *what* you did, but never *how*. 


#### Use `TODO` and `FIXME` tags.
Comment unfinished work with `TODO:` or `FIXME:`, which allows to search & find these lines later. A `TODO` is more urgent and needs to be done, a `FIXME` would be nice to have but is not required.


#### Readme Files
There are two different interest groups for your code, so please make sure that your Readme addresses both.

 * **Users:** How to install and run your code with examples. Supported OS. Release versions and change logs.
 * **Developers:** How to compile. Module structure, dependencies, contribution rules, where to contact developers.  





&nbsp;
## [Languages](chapter/6_languages.md)
Each programming language has special mechanisms and some rules are only applicable to a certain language. Click on the following links to get to the main article for each language.

* **[Python](chapter/lang/python-guide.md)**
* **[C](chapter/lang/c-guide.md)**






&nbsp;
## References
This guide is based on the principles that are explained in the following documents and books and we can recommend them as further reading material.

 * [1] G. Van Rossum, B. Warsaw, and N. Coghlan: “PEP 8: Style Guide for Python Code”, Python.org, vol. 1565, 2001.
 * [2] S. McConnell: “Code Complete”, Pearson Education, 2004.
 * [3] R. C. Martin: “Clean Code: A Handbook of Agile Software Craftsmanship”, Pearson Education, 2009.
 * [4] R. C. Martin: “Clean Architecture: Guide to Software Structure and Design”, Pearson Education, 2017.
 * [5] E. Freeman et. al.: “Head First Design Patterns”, O’Reilly Media, 2008.

