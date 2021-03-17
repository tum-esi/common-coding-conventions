
## Naming Suggestions
Code should communicate behavior to other humans with lower complexity than the behavior it inherits. Abstracting with meaningful names is most important for readability.


#### Subprograms (=Procedure/Function)
Procedures *may* return values, functions always return a value. Methods are subprograms of a class.
 * procedure names should start with a verb. e.g. `syncViews()`, `list.addItem(x)`.
 * function names should describe the result and, if suitable, its type. e.g. `time_ms(), sin(x)`
 * returning procedures can do both. e.g. `fh = openFileAndGetHandler(path)`
 * class methods should not repeat or include the name of the class. Define `Line.length()`, not `Line.getLineLength()`

*Single noun subprograms must be pure functions! Never let e.g. `x.length()` change a state.*


#### Types (=Class/Struct/Subtypes)
 * type names should be capitalized nouns. E.g. `Integer`, `Date`, `Line2D`
 * Enums/Structs are types and named as types without a special prefix/suffix.
 * Interface names should start with a capital `I` and can also be adjectives. E.g. `IObservable`
 * create own (sub)types for physical units. E.g. `Meter` and `Second` from `Float`
 * Distinguish between class name suffixes:
   * `Factory`/`Builder`: creates objects and transfers ownership (e.g. to a Manager).
   * `Manager`: stateless, owns and provides access to same-type objects (e.g. `SensorManager`).
   * `Controller`: stateful, handles communication between different objects (e.g. `FlightController`).
   * `Handler`: waits for and processes a single-type object, without owning it (e.g. `EventHandler`).


#### Variables
 * variables with a large scope *should* have long names, variables with a small scope *can* have short names.
 * collections (set, array, dict) should have a plural name. E.g. `cars`, `indices`
 * the prefix `n` or `num` should be used for names representing the total number of objects in a collection. E.g. `nCars`
 * boolean variables should start with a `is/has/can/does` prefix (e.g. `isEmpty`, `doesUseIO`).
 * write constant names in capitals. E.g `CFG_TEMPERATURE_MAX = 80.0`
 * prefix global and static variables with `g_` and `s_`


**Bad**
```
score_list = [0] * scores 
for	idx, val in score_list:
score_list = val + 1
```

**Better**
```
scores = [0] * numScores 
for	idx, score in scores:
scores[idx] = score + 1
```


#### High-level Scopes (= Module/Package/Namespace)
The names for packages or namespaces, which should prevent name clashes, should be short as they are used often within the code.
In this case, choosing an abbreviation or acronym makes sense.

#### Use abbreviations cautiously and only common ones.
To abbr. or not to abbreviate? Truth is, neither `GetTheLatestWebSiteAccessTimeInMilliseconds()`, nor `pm_rcv_bat_stat()` are reader friendly. 
Use abbreviations only for small scopes, function arguments, or in combination with full names (`move_cmd`).
Avoid abbreviations if they
only save one character (`usr`), are too cryptic (`cmp`), or can be confused with other terms (`tmp`).
If you use them, stick to the following common abbreviations (already a lot):


<!-- <div class="row">
<div class="col">
 -->

| **Abbr.**  | **Meaning**  |
|--------|-------|
| `arg`  |  argument  |
| `app`  |  application  |
| `auth` |  authentication  |
| `avg`  |  average  |
| `bat`  |  battery  |
| `buf`  |  buffer  |
| `cb`   |  callback  |
| `cfg`  |  config.  |
| `clk`  |  clock  |
| `col`  |  column  |
| `cnt`  |  counter  |
| `cmd`  |  command  |
| `ctx`  |  context  |
| `dev`  |  device  |
| `doc`  |  document  |
| `drv`  |  driver  |
| `dt`   |  delta time  |
| `el`   |  element  |
| `env`  |  environment  |
| `err`  |  error  |
| `exc`  |  exception  |

<!-- </div>
<div class="col"> -->

| **Abbr.** | **Meaning**  |
|--------|-------|
| `fh`   |  file handler  |
| `fmt`  |  format  |
| `hdr`  |  header  |
| `hex`  |  hexadecimal  |
| `img`  |  image  |
| `idx`  |  index  |
| `len`  |  length  |
| `lib`  |  library  |
| `lvl`  |  level  |
| `max`  |  maximum  |
| `mid`  |  middle  |
| `min`  |  minimum  |
| `mem`  |  memory  |
| `mon`  |  monitor  |
| `msg`  |  message  |
| `net`  |  network  |
| `num`  |  number  |
| `obj`  |  object  |
| `pkg`  |  package  |
| `pkt`  |  packet  |
| `pos`  |  position  |
| `pt`   |  point  |
| `ptr`  |  pointer  |
| `pwr`  |  power  |
| `px`   |  pixel  |
| `rnd`  |  round  |
| `reg`  |  register  |
| `rot`  |  rotation  |
| `sep`  |  separator  |
| `std`  |  standard  |
| `str`  |  string  |
| `sys`  |  system  |
| `tmr`  |  timer  |
| `ts`   |  timestamp  |
| `val`  |  value  |
| `var`  |  variable  |
| `win`  |  window  |

<!-- </div>
</div> -->

Per-second/minute acronyms: `fps` (frame), `rpm` (rotations), `mps` (meter)
Avoid these abbr.: `tmp`, `fun`, `chk`, `dis`, `usr`, `cpy`, `tgl`, `txt`, `pc`, `mov`, `sec`


###### Domain Specific Abbreviations and Acronyms for Embedded Systems:
 * Sensors: `IMU` (=`ACC`, `GYR`, `MAG`), `BARO`, `TEMP`, `GPS` (= `lat`, `lon`, `alt`)
 * Buses: `USB`, `CAN`, `SPI`, `I2C`, `UART`, `ETH`, `PCI`
 * Processor: `CPU`, `GPU`, `MCU`: `RAM`, `ROM`, `ISR`, `ADC`, `DAC`, `RTC`, `CLK`, `DMA`
 * Software: `API`, `CLI`, `GUI`, `HAL`, `OS`, `VM`, `PID`, `UID`, `LSB`, `MSB`, `CRC`



#### Use word pairs (opposites, antonyms)
If you “`start`” something, you should “`stop`” it and not “`end`” it. While most opposites can be created by using `un-` or `de-` prefixes (`lock/unlock`), some are more distinct and allow vertical code alignment:

Verb pairs with same length:

| `set` |`send` |`query` |`init`  |`insert` |`attach` |`inc` |`show` |`split` |`enter` |`accept`  |
|-------|-------|--------|--------|---------|---------|------|-------|--------|--------|----------|
| `get` |`recv` |`reply` |`fini`  |`delete` |`detach` |`dec` |`hide` |`merge` |`leave` |`reject`  |


Verb pairs that differ by one character are more visually distinct but still easy to align with one extra space:


|  `open`  | `read`  | `load`  | `push` | `start` | `create`  | `grant` | `hit`  | `prepend` | `empty`  |
|----------|---------|---------|--------|---------|-----------|---------|--------|-----------|----------|
|  `close` | `write` | `store` | `pop`  | `stop`  | `destroy` | `deny`  | `miss` | `append`  | `full`   |


Noun pairs with same/similar length:

| `max` |`next` |`head` |`new` |`row` |`ack` |`source` |`client` |`primary` |`front` |`leader` |
|-------|-------|-------|------|------|------|---------|---------|----------|--------|----------|
| `min` |`prev` |`tail` |`old` |`col` |`nak` |`target` |`server` |`replica` |`back`  |`follower` |


Avoid inappropriate terms: `master/slave`. See [1](https://www.drupal.org/node/2275877) and [2](https://bugs.python.org/issue34605).
