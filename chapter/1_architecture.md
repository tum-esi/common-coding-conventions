
## Additional Architecture Rules

[Read base rules.](../Readme.md#user-content-architecture)


### Be open for extension, but closed for modification.

If you need to add a new feature (logic), the architecture should only
be extended with no or little modification. How? Separate class methods
that could have several behaviors and encapsulate them behind a new
interface. Creating multiple, specific interfaces is better than one
giant, general-purpose interface that needs to change. Ask yourself: If
you add a new class (e.g. new feature) to your design, how many classes
have to change?


### Separate models from views and control (MVC).

A model (program logic+states) is the heart of each module and
operations on the open heart are dangerous. Therefore, larger modules
should protect the model from

* direct input by having a controller that preprocesses requests
* direct output by having one or more views that provide different output formats

External modules can access the controller (if they want to change the
model's state) or access the views (if they want to know the model's
state). See
[MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller).


### Depend on abstractions, not implementations

Abstract superclasses and interfaces allow you to hide implementation
details, which reduces dependencies. In UML, associations between
semantically different objects should preferably point to interfaces,
instead of concrete classes. In code, statements such as `include` or
`import` should mostly bring interfaces and abstract classes into the
scope. E.g. instead of calling `display3.setLED(2, red)` directly, use
an abstract `GUI.warnUser()`. If you depend on concrete classes, make
sure they are small, singletons, closely related, or really stable (e.g.
`String` in Java).