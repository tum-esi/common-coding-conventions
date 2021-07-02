## Additional Naming Suggestions

[Read base rules.](../README.md#user-content-naming)



### Class Name Suffixes

Class names often have a suffix term that indicates the purpose (and not only the topic) of that class. While there seems to be no common agreement on the notation, we find the following distinction useful:

* `Factory`/`Builder`: creates objects and transfers ownership (e.g. to a Manager).
* `Manager`: stateless, owns and provides access to same-type objects (e.g. `SensorManager`).
* `Controller`: stateful, handles communication between different objects (e.g. `FlightController`).
* `Handler`: waits for and processes a single-type object, without owning it (e.g. `EventHandler`).



### High-level Scopes (= Module/Package/Namespace)

The names for packages or namespaces, which should prevent name clashes, should be short as they are used often within the code. In this case, choosing an abbreviation or acronym makes sense.



### Use physical units as type names.

In embedded systems, you often have to deal with physical quantities. To make clear which unit a certain variable has, you should define your own (sub)types for physical units based on numerical type, such as `Meter` and `Second` from `Float`, and then declare variables as `Meter safety_distance = 5.0;`. 



### Use abbreviations cautiously and only common ones.

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
<summary>👆 <strong>List of Domain Specific Abbreviations</strong></summary>

### Abbreviations and Acronyms in Embedded Systems:

 * Sensors: `IMU` (=`ACC`, `GYR`, `MAG`), `BARO`, `TEMP`, `GPS` (= `lat`, `lon`, `alt`)
 * Buses: `USB`, `CAN`, `SPI`, `I2C`, `UART`, `ETH`, `PCI`
 * Processor: `CPU`, `GPU`, `MCU`: `RAM`, `ROM`, `ISR`, `ADC`, `DAC`, `RTC`, `CLK`, `DMA`
 * Software: `API`, `CLI`, `GUI`, `HAL`, `OS`, `VM`, `PID`, `UID`, `LSB`, `MSB`, `CRC`

</details>

