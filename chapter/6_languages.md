## Language Specific Advice 


### Python

#### OOP in Python
 * Use `raise NotImplementedError` to indicate abstract methods.
 * private attributes/functions should start with `_` in their name, e.g. `_secret`
 * Create own types by assigning a base type to a name, e.g. `Volt = float`

#### General Coding
 * Separate large numbers with underscores. Prefer `1_000_000` over `1000000`.
 * Use `_` for unused variables: `_, extension = 'foobar.txt'.split('.')`
 * constants are indicated by all uppercase names.

#### Further down the Pythonic road
 * Use context managers when reading files or acquiring locks/semaphores:\\ `with open('file.txt', 'r') as f:`
 * Use for-loops that iterate over what you actually need:
 * Elements: `for car in cars:`
 * Index and Element: `for idx, car in enumerate(cars):`
 * Elements of multiple lists: `for car, driver in zip(cars, drivers):`


**Example**
```python
class Employee(Person):           # inheritance
  count = 0                       # static attr. (shared by all instances)

  def __init__(self, name: str):  # constructor
     super().__init__()
     Employee.count += 1
     self.name = name             # local attr. (local to one instance)
  
     print(Employee.count)
```

