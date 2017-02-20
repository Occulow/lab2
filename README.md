# Description
This repository holds everyting you need to complete 18-549 Lab2.

# Software Dependencies
* `avr-libc` (version 1.8 works), `binutils-avr`, `gcc-avr`
  On Debian or Ubuntu
* `avrdude` version 6.2 or later
* `minicom`

On more recent verison of Debian and Ubuntu you should be able to do the following:
```
sudo apt-get update
sudo apt-get install avr-libc avrdude minicom
```

# Programming
This lab requires you to flash the bootloader and then a UART test program,
using the bootloader.

To flash the bootloader you need an Atmel ICE In System Programmer(ISP)
and avrdude. Once you have the bootloader flashed, you can load the UART
test program using avrdude and a basic USB to serial cable(FTDI cable).

We support two different Atmega328P designs, the 8MHz(for 3.3V) and the
16MHz(for 5V). On this MCU, hardware peripheral(like uart) configuration
and core system libraries are dependent on the clock rate.
For this reason, you must ensure that the software being compiled for
your MCU is aware of the chosen clock rate. This is typically set at
compile time using the `F_CPU` macro. The instructions below show
how you set the clock rate for the build system.

Here are the specific commands for each clock rate:

* 16MHz clock [default design] <br />
  In the `arduino_bootloader` directory run the following command:
  ```
  make atmega328_isp
  ```
  In the `uart_test` directory run the following commands:
  ```
  make
  make program
  ```
* 8MHz clock <br />
  In the `arduino_bootloader` directory run the following command:
  ```
  make atmega328_pro8_isp
  ```
  In the `uart_test` directory run the following commands:
  ```
  make AVR_FREQ=8000000L
  make program
  ```

# Testing
Open minicom on /dev/ttyUSB0.
Ensure that you see "Hello World" first, then you see an echo of all keys that your type.

# Extra Notes
The Debian install command should be sufficient, since avr-libc depends
on all of the other AVR tools.
A changelog entry mentioned that AtmelICE support was added in
version 6.2. Testing shows it working on avrdude version 6.3.