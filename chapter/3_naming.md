
## Naming Suggestions


Code should communicate behavior to other humans with lower complexity than the behavior it inherits. Abstracting with meaningful names is therefore most important for readability.

> ⚠ **Avoid inappropriate terms:** Many organizations discourage the use of `master/slave` due to their negative association in different cultures. See [1](https://www.drupal.org/node/2275877) and [2](https://bugs.python.org/issue34605).


### Subprograms (=Procedure/Function)
Procedures *may* return values, functions always return a value. Methods are subprograms of a class.
 * procedure names should start with a verb. e.g. `syncViews()`, `list.addItem(x)`.
 * function names should describe the result and, if suitable, its type. e.g. `time_ms(), sin(x)`
 * returning procedures can do both. e.g. `fh = openFileAndGetHandler(path)`
 * class methods should not repeat or include the name of the class. Define `Line.length()`, not `Line.getLineLength()`

> ⚠ **Caution:** *Single noun subprograms should be pure functions! Never let e.g. `x.length()` change a state.*



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
 * prefix global variables with `g_`


<table>
<tr><td><strong>Bad ❌</strong></td><td><strong>Better ✔</strong></td></tr>
<tr>
<td>

```python
score_list = [0] * scores 
for	idx, val in score_list:
	score_list = val + 1
```

</td><td>

```python
scores = [0] * numScores 
for	idx, score in scores:
	scores[idx] = score + 1
```

</td></tr></table>


#### High-level Scopes (= Module/Package/Namespace)
The names for packages or namespaces, which should prevent name clashes, should be short as they are used often within the code.
In this case, choosing an abbreviation or acronym makes sense.


#### Use abbreviations cautiously and only common ones.
To abbr. or not to abbreviate? Truth is, neither `GetTheLatestWebSiteAccessTimeInMilliseconds()`, nor `pm_rcv_bat_stat()` are reader friendly. 
Use abbreviations only for small scopes, function arguments, or in combination with full names (`move_cmd`).
Avoid abbreviations if they only save one character (`usr`), are too cryptic (`cmp`), or can be confused with other terms (`tmp`). If you use them, stick to the following common abbreviations (already a lot):

<details>
<summary>👆 <strong>List of common coding abbreviations</strong>
</summary>

| **Abbr.**  | **Meaning** |   | **Abbr.**  | **Meaning** |
|--------|-----------------|---|--------|------------|
| `arg`  |  argument       |   | `mid`  |  middle    |
| `app`  |  application    |   | `min`  |  minimum   |
| `auth` |  authentication |   | `mem`  |  memory    |
| `avg`  |  average        |   | `mon`  |  monitor   |
| `bat`  |  battery        |   | `msg`  |  message   |
| `buf`  |  buffer         |   | `net`  |  network   |
| `cb`   |  callback       |   | `num`  |  number    |
| `cfg`  |  config.        |   | `obj`  |  object    |
| `clk`  |  clock          |   | `pkg`  |  package   |
| `col`  |  column         |   | `pkt`  |  packet    |
| `cnt`  |  counter        |   | `pos`  |  position  |
| `cmd`  |  command        |   | `pt`   |  point     |
| `ctx`  |  context        |   | `ptr`  |  pointer   |
| `dev`  |  device         |   | `pwr`  |  power     |
| `doc`  |  document       |   | `px`   |  pixel     |
| `drv`  |  driver         |   | `rnd`  |  round     |
| `dt`   |  delta time     |   | `reg`  |  register  |
| `el`   |  element        |   | `rot`  |  rotation  |
| `env`  |  environment    |   | `sep`  |  separator |
| `err`  |  error          |   | `std`  |  standard  |
| `exc`  |  exception      |   | `str`  |  string    |
| `fh`   |  file handler   |   | `sys`  |  system    |
| `fmt`  |  format         |   | `tmr`  |  timer     |
| `hdr`  |  header         |   | `ts`   |  timestamp |
| `hex`  |  hexadecimal    |   | `val`  |  value     |
| `img`  |  image          |   | `var`  |  variable  |
| `idx`  |  index          |   | `win`  |  window    |
| `len`  |  length         |
| `lib`  |  library        |
| `lvl`  |  level          |
| `max`  |  maximum        |


Per-second/minute acronyms: `fps` (frame), `rpm` (rotations), `mps` (meter)
Avoid these abbr.: `tmp`, `fun`, `chk`, `dis`, `usr`, `cpy`, `tgl`, `txt`, `pc`, `mov`, `sec`

</details>&nbsp;




<details>
<summary>👆 <strong>List of Domain Specific Abbreviations</strong>
</summary>

### Abbreviations and Acronyms in Embedded Systems:
 * Sensors: `IMU` (=`ACC`, `GYR`, `MAG`), `BARO`, `TEMP`, `GPS` (= `lat`, `lon`, `alt`)
 * Buses: `USB`, `CAN`, `SPI`, `I2C`, `UART`, `ETH`, `PCI`
 * Processor: `CPU`, `GPU`, `MCU`: `RAM`, `ROM`, `ISR`, `ADC`, `DAC`, `RTC`, `CLK`, `DMA`
 * Software: `API`, `CLI`, `GUI`, `HAL`, `OS`, `VM`, `PID`, `UID`, `LSB`, `MSB`, `CRC`

</details>



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



