# OneWire Library
This is just a mirror from [Teensyduino](http://www.pjrc.com/teensy/td_libs_OneWire.html)

OneWire lets you access 1-wire devices made by Maxim/Dallas, such as temperature sensors and ibutton secure memory. For temperature sensors, the DallasTemperature library can be used in conjunction with this library.

## Hardware Requirements
OneWire requires a single 4.7K pullup resistor, connected between the pin and +5 volts. Then just connect each 1-wire device to the pin and ground. Some 1-wire devices can also connect to power, or get their power from the signal wire. Please refer to the specifications for the 1-wire devices you are using.

## Basic Usage
```
OneWire myWire(pin);
```
Create the OneWire object, using a specific pin. Even though you can connect many 1 wire devices to the same pin, if you have a large number, smaller groups each on their own pin can help isolate wiring problems. You can create multiple OneWire objects, one for each pin.

```
myWire.search(addrArray);
```
Search for the next device. The addrArray is an 8 byte array. If a device is found, addrArray is filled with the device's address and true is returned. If no more devices are found, false is returned.

```
myWire.reset_search();
```
Begin a new search. The next use of search will begin at the first device.

```
myWire.target_search(family_code);
```
Setup the search to find the device type 'family_code' on the next call to search(*newAddr) if it is present.

```
myWire.reset();
```
Reset the 1-wire bus. Usually this is needed before communicating with any device.

```
myWire.select(addrArray);
```
Select a device based on its address. After a reset, this is needed to choose which device you will use, and then all communication will be with that device, until another reset.

```
myWire.skip();
```
Skip the device selection. This only works if you have a single device, but you can avoid searching and use this to immediatly access your device.

```
myWire.write(num);
```
Write a byte.

```
myWire.write(num, 1);
```
Write a byte, and leave power applied to the 1 wire bus.

```
myWire.read();

```
Read a byte.

```
myWire.crc8(dataArray, length);
```
Compute a CRC check on an array of data.

## 1-Wire Information
* [Maxim Semiconductor's 1-Wire Products](http://www.maxim-ic.com/products/1-wire/)
* [Wikipedia explains 1-wire protocol](http://en.wikipedia.org/wiki/1-Wire)
* [Tom Boyd explains 1-wire protocol](http://www.arunet.co.uk/tkboyd/e1didx.htm)
* [Dallas Temperature Control Library](http://milesburton.com/index.php?title=Dallas_Temperature_Control_Library)
* [Arduino's OneWire page (warning: has buggy version)](http://www.arduino.cc/playground/Learning/OneWire)
* [Weather Toys - community using 1-wire devices.](http://www.weathertoys.net/weathertoys/main.html)

## History & Credits
* Jim Studt wrote OneWire in 2007, originally based on code by Derek Yerger.
* Tom Pollard added CRC code which eliminated the need for a 256 byte array (in RAM).
* "RJL20" added the skip function.
* Robin James rewrote the search function, posting his version [here](http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1238032295/27#27).
* Paul Stoffregen rewrote the I/O routines for interrupt safety, replaced search with Robin James's code, applied several small optimizations, and started calling it "version 2.0" to distinguish from the many buggy copies online. 
