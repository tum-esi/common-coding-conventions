
## Documentation
English is the language of programming, so documentation should also be only English.


#### Comments
Comments that contradict the code are worse than no comments. Change comments when code changes.
Comment only what the code cannot say, that is *why* you did it, maybe *what* you did, but never *how*. 


#### File Header
Each code file should start with a block comment that states what this module/class/lib does and author contact.


#### Readme Files
There are two different interest groups for your code and it is very frustrating if you only address one. Please make sure that your Readme covers both.

 * **Users:** How to install and run your code with examples. Supported OS. Release versions and change logs.
 * **Developers:** How to compile. Module structure, dependencies, contribution rules, where to contact developers.  


#### Use `TODO` and `FIXME` tags.
Comment unfinished work with `TODO:` or `FIXME:`, which allows to search & find these lines later. A `TODO` is more urgent and needs to be done, a `FIXME` would be nice to have but is not required.


#### Docstrings
Docstrings are specially formatted comments that can be converted into a code documentation. Docstrings require effort to maintain, so they are intended and suitable for larger, popular frameworks like Qt or OpenCV.



