## Safety and Security

Both topics are very complex and thus cannot and shall not be covered in detail in this guide. 
However, they are important, so you should have a basic understanding of how this affects your code.

**Safety** is in general achieved by 

* limiting certain language constructs,
* testing and static analysis,
* inspection and validation by other people.

**Security** is achieved by

* using cryptography such as encryption, signatures, and hashes
* careful management of the involved keys (where/how to store)
* relying on well-established libraries and never implementing own crypto



### Safety Rules

#### Validate any external input.

Do not make any assumption about input variables that you do not have control of. This means that you should perform range checks before further processing variable. E.g. if your function requires a length argument, check that is a positive value and smaller than the largest value your function can handle.

```python
if 0 <= x.len <= LEN_MAX: raise ValueError
```



#### All loops must have fixed bounds.

Instead of a simple `while(cond)` loop, provide a fixed number of retries, e.g. `while(cond && retries < 5)`. This will prevent that your program gets stuck in an infinite loop.



#### Check the return value of all non-void functions.

Never assume that functions will return successfully because they do so most of the time.



