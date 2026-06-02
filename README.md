# amalgame-hardware-io

Portable **I/O expander** drivers for Amalgame over [`amalgame-hal`](https://github.com/amalgame-lang/amalgame-hal). A PCF8574 adds 8 digital pins on two I²C wires; each pin is a `DigitalOut` **and** `DigitalIn`, so it drops into any driver (LEDs, relays, buttons, LCD backpacks…).

```sh
amc package add hardware-io
```

```amalgame
import Amalgame.Hardware          // I2c (Pi backend)
import Amalgame.Hardware.Io
import Amalgame.Hardware.Led

let exp = new Pcf8574(new I2c(1), 0x20)
let led = new Led(exp.Pin(0))     // expander pin → DigitalOut
led.On()
let pressed = exp.Pin(1).Read()   // … or as a DigitalIn
```

| Class | API |
|---|---|
| `Pcf8574(bus: I2cBus, addr)` | `WritePin(pin, high)`, `ReadPin(pin)`, `Pin(n)` |
| `Pcf8574Pin` | `implements DigitalOut, DigitalIn` — `Write/High/Low/Toggle/Read` |

Requires amc ≥ 0.8.72. Apache-2.0.
