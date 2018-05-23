# MicroPython MAX7219 8x8 LED Matrix

A MicroPython library for the MAX7219 8x8 LED matrix driver, SPI interface, supports cascading and uses [framebuf](http://docs.micropython.org/en/latest/pyboard/library/framebuf.html)

## PyBoard Examples

**Single 8x8 LED Matrix**

```
import max7219
from machine import Pin, SPI
spi = SPI(1)
display = max7219.Matrix8x8(spi, Pin('X5'), 1)
display.text('1',0,0,1)
display.show()
```

**Chain of 4x 8x8 LED Matrices**
Where the 4 is drawn on the DIN matrix.

```
import max7219
from machine import Pin, SPI
spi = SPI(1)
display = max7219.Matrix8x8(spi, Pin('X5'), 4)
display.text('1234',0,0,1)
display.show()
```

**Chain of 8x 8x8 LED Matrices**
Where the 8 is drawn on the DIN matrix

```
import max7219
from machine import Pin, SPI
spi = SPI(1)
display = max7219.Matrix8x8(spi, Pin('X5'), 8)
display.text('12345678',0,0,1)
display.show()
```

**Framebuf shapes and text**

```
display.fill(0)
display.show()

display.pixel(0,0,1)
display.pixel(1,1,1)
display.hline(0,4,8,1)
display.vline(4,0,8,1)
display.line(8, 0, 16, 8, 1)
display.rect(17,1,6,6,1)
display.fill_rect(25,1,6,6,1)
display.show()

display.fill(0)
display.text('dead',0,0,1)
display.text('beef',32,0,1)
display.show()

display.fill(0)
display.text('12345678',0,0,1)
display.show()
display.scroll(-8,0) # 23456788
display.scroll(-8,0) # 34567888
display.show()
```

## ESP8266 Examples

Default baud rate of 80Mhz was introducing errors, dropped from 10Mhz and it works consistently.

**Single 8x8 LED Matrix**

```
import max7219
from machine import Pin, SPI
spi = SPI(1, baudrate=10000000, polarity=0, phase=0)
display = max7219.Matrix8x8(spi, Pin(15), 1)
display.text('1', 0, 0, 1)
display.show()
```

**Chain of 4x 8x8 LED Matrices**
Where the 4 is drawn on the DIN matrix.

```
import max7219
from machine import Pin, SPI
spi = SPI(1, baudrate=10000000, polarity=0, phase=0)
display = max7219.Matrix8x8(spi, Pin(15), 4)
display.brightness(0)
display.fill(0)
display.text('1234', 0, 0, 1)
display.show()
```

## Pin Connections

PyBoard | max7219 8x8 LED Matrix
------- | ----------------------
VIN     | VCC
GND     | GND
X8 MOSI | DIN
X5 CS   | CS
X6 SCK  | CLK

Wemos D1 Mini    | max7219 8x8 LED Matrix
---------------- | ----------------------
5V               | VCC
GND              | GND
D7 MOSI (GPIO13) | DIN
D8 CS (GPIO15)   | CS
D5 SCK (GPIO14)  | CLK

NodeMCU          | max7219 8x8 LED Matrix
---------------- | ----------------------
VIN              | VCC
GND              | GND
D7 (GPIO13)      | DIN
D8 (GPIO15)      | CS
D5 (GPIO14)      | CLK

## Links

* Based on [deshipu's max7219.py](https://bitbucket.org/thesheep/micropython-max7219/src)
* [micropython.org](http://micropython.org)
* [Docs on framebuf](http://docs.micropython.org/en/latest/pyboard/library/framebuf.html)
