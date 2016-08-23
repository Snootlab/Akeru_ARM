Akeru - TD1208 library for Arduino
=========

Requirements
------------

[Akeru](http://snootlab.com/lang-en/snootlab-shields/829-akeru-beta-33-en.html)

or

[Arduino/Genuino Uno](http://snootlab.com/lang-en/arduino-genuino-en/956-genuino-uno-arduino-uno-en.html) + [Akene](http://snootlab.com/lang-en/snootlab-shields/889-akene-v1-en.html) or [TD1208 Breakout](http://snootlab.com/lang-en/snootlab-shields/962-breakout-td1208-connectivity-1-year-accessories-en.html)

Examples
--------

* DemoTest : full demo sketch
  * Checks if the modem is available
  * reads temperature, supply voltage, hardware & firmware version, power level
  * sends temperature & supply voltage on Sigfox network
* downlinkDemo : how to receive data from the Sigfox network
* sendMultipleValues : sending various values in a single message
* sendSingleValues  : sending values from a single analog sensor 

Installation
------------

Like any other library, see [tutorial](http://arduino.cc/en/Hacking/Libraries)

Use
--------------------------------------

####Sigfox module initialization

ARM boards do not support SoftwareSerial library, but have a few hardware serial ports available. There's a single library file to include and a simple line of code to map the signals according to your device :

```
#include <Akeru.h>

Akeru akeru(&Serial1); // D0+D1
```

Port mapping :

Serial port | RX  | TX 
----------  | --- | ---
Serial1     | D0  | D1
Serial2     | D12 | D10
Serial3     | D5  | D2

In order to use Serial2 & Serial3 you'll need to modify 2 files, see [tutorial](http://forum.snootlab.com/viewtopic.php?f=51&t=1514) on our forum (in french).

####Powering up

A single line to add in your `void setup()` :

```
akeru.begin(); // returns 1 when everything went ok
```

####Enabling/Disabling echo

To see AT commands and their answers : `akeru.echoOn();`

To hide AT commands and their answers : `akeru.echoOff();`

####Sending data

Data is sent to the Sigfox network in hexadecimal format, and the payload has to be a String of all elements you want to send. To ensure proper conversion of your variables, you can use `akeru.toHex()` method :

```
int val = analogRead(0);
String valString = akeru.toHex(val);
akeru.sendPayload(varString);
```
Note that if you send a array of `char` you need to provide its size in order to convert it :
```
char array[] = "Hello world";
String arrayString= akeru.toHex(array, sizeof(array));
akeru.sendPayload(arrayString);
```

Documentation
-------------

Visit [our specific forum](http://forum.snootlab.com/viewforum.php?f=51) !
Read the full documentation [in french](http://forum.snootlab.com/viewtopic.php?f=51&t=1508) or [in english](http://forum.snootlab.com/viewtopic.php?f=51&t=1509).
