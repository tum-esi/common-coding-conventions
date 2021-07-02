## Additional Clarifications 


### Apply OOP

One method to maintain complexity is abstraction and encapsulation using
classes and interfaces. Although, not every part of your software design
fits well into an object, humans can easily understand objects with
attributes and methods and their relations to each other. 


* **Encapsulation:** Group related attributes and methods.
* **Abstraction:** Provide high-level interfaces, hide details.
* **Inheritance:** Derive classes from other classes (hierarchy).
* **Polymorphism:** Overwrite derived methods to change behavior.



### Use Unified Modeling Language (UML)
UML is great when trying to plan or explain architecture and code structure.
Possible UML relations between objects:


| **Relation**  | **Description** (P: parent, C: child)     | **Example P** | rel.| **Example C** |
| --------------|:------------------------------------------|---------:|:--------:|:--------------|
| Association:  | "P may use a C. C may belong to P"        |    Human | ––––––   | Computer      |
| Dependency:   | "P depends on C. C provides for P"        |    Human | - - - -> | Food          |
| Aggregation:  | "Group P has a C. C is assigned to P"     |  Company | ◇–––––   | Human         |
| Composition:  | "P is made of C. C is part of every P"    |    Human | ◆–––––   | Leg           |
| Realization:  | "P abstracts C. C implements P."          |    Human | ◁- - - - | Socrates      |
| Inheritance:  | "P is the class of C. Every C *is a* P."  |   Mammal | ◁–––––   | Human         |


> :warning: **Aggregation vs. Composition:** If you remove the composition you will also
> remove the children, but if you remove the aggregate the children still
> exist. Remove the company and you still have humans, remove the human
> and you also remove his/her legs.

