
## Architecture

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

**Better**
```python
Sys.test():
 Engine.test():
  SparkPlug.test():
   testIgnition()
```

*Mixing abstraction level creates confusion and introduces unnecessary
dependencies.*


#### Aim for low coupling between classes

You may have many classes but each class should communicate with as few
others as possible. If any two classes communicate at all, they should
exchange as little information as possible.

Data classes should only be changed by a single supervisor class or
passed on in a strict [Chain of Responsibility](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern).
If two independent classes write to the same data class, the risk for
conflicts increases.



#### Separate models from views and control (MVC).

A model (program logic+states) is the heart of each module and
operations on the open heart are dangerous. Therefore, larger modules
should protect the model from

External modules can access the controller (if they want to change the
model's state) or access the views (if they want to know the model's
state). See
[MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller).


#### Depend on abstractions, not implementations

Abstract superclasses and interfaces allow you to hide implementation
details, which reduces dependencies. In UML, associations between
semantically different objects should preferably point to interfaces,
instead of concrete classes. In code, statements such as `include` or
`import` should mostly bring interfaces and abstract classes into the
scope. E.g. instead of calling `display3.setLED(2, red)` directly, use
an abstract `GUI.warnUser()`. If you depend on concrete classes, make
sure they are small, singletons, closely related, or really stable (e.g.
`String` in Java).



#### Be open for extension, but closed for modification.

If you need to add a new feature (logic), the architecture should only
be extended with no or little modification. How? Separate class methods
that could have several behaviors and encapsulate them behind a new
interface. Creating multiple, specific interfaces is better than one
giant, general-purpose interface that needs to change. Ask yourself: If
you add a new class (e.g. new feature) to your design, how many classes
have to change?
