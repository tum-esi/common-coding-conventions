### C Specific Advice

#### Object Oriented Programming in C

C does not support real OOP but the following rules can help to transfer some ideas of OOP to C.

* **Think of a file as a class:** Functions that appear in the header file are public, while functions that only appear in the `.c` files are private.

* **Create namespaces:** use a capital prefix before each “public” function name to indicate their belonging to a certain source file. For example, in `led.c` use `LED_switchOn( redLed );` instead of `switchOn(redLed)`

* **Use structs to encapsulate attributes:** Instead of individual variables, group variables that would belong to a class in a struct. You can then pass a reference of this struct as the first argument to a function.


#### Further

* **Constants**: for constants prefer `const` over preprocessor `#define`
* **Booleans**: Use `bool` from `stdbool.h` whenever you have a boolean value
* **Sizeof**: use `sizeof` on the variable; not the type
