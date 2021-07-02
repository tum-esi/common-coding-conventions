## Code Layout (Visual Appearance)
A clear and consistent visual appearance of your code improves readability and readability helps to understand the code.

 * Existing Project: Stick to the existing recommendation and tools.
 * New Project: Use an automatic code layouter. Examples:


| Language   | Tool                                                        |   
|:-----------|-------------------------------------------------------------|
| C          | [uncrustify](http://uncrustify.sourceforge.net/)            |
| C++        | [clang-format](http://clang.llvm.org/docs/ClangFormat.html) |
| Python     | [black](https://pypi.org/project/black/)                    |
| JavaScript | [prettier.io](https://prettier.io/)                         |


Here are some example recommendations that would be ensured by most layouters:

 * aim for one statement and less than 80 characters per line
 * indent with spaces not tabs because editors do not agree on tab width
 * surround top-level function and class definitions with two or three blank lines.
 * surround binary operators (=, ==, +) with a single space, except when nested inline
 * break lines before operators and align operators vertically

