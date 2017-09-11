# Itho-WIFI-remote-Homey
Cloned from https://github.com/incmve/Itho-WIFI-remote, which was cloned from https://github.com/supersjimmie/IthoEcoFanRFT. This version just adds integration with the Homey domotics controller.

--
I used A CC1101 module, might work with others like CC1150.
```
Connections between the CC1101 and the ESP8266:
CC11xx pins    ESP pins   		Description
*  1 - VCC        VCC         	3v3
*  2 - GND        GND     		Ground
*  3 - MOSI       13=D7  		Data input to CC11xx
*  4 - SCK        14=D5			Clock pin
*  5 - MISO/GDO1  12=D6			Data output from CC11xx / serial clock from CC11xx
*  6 - GDO2       ? 			Programmable output
*  7 - GDO0       ?  			Programmable output
*  8 - CSN        15=D8 		Chip select / (SPI_SS)
```


Beware that the CC11xx modules are 3.3V (3.6V max) on all pins!
This won't be a problem with an ESP8266, but for Arduino you either need to use a 3.3V Arduino or use levelshifters and a separate 3.3V power source.

For SPI, pins 12-15 ()aka D5-D8) are used, a larger ESP8266 model like (but not only) the ESP-03, ESP-07, ESP-12(D, E) or a NodeMCU board is required.

Added a web interface and simple API to control it from the Homey domotics controller (https://athom.com).

![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/itho-contro-panel.png)

Also able to give commands by USB (serial)

![alt tag](https://github.com/incmve/Itho-WIFI-remote/blob/master/Images/serial.JPG)


The API works like this:
```
http://192.168.x.x/api?action=Low
http://192.168.x.x/api?action=Medium
http://192.168.x.x/api?action=High
http://192.168.x.x/api?action=Timer
http://192.168.x.x/api?action=Learn
http://192.168.x.x/api?action=reset&value=true
Added:
http://192.168.x.x/api?action=State
```

The following screenshots show how the Homey 'flows' are built using the 'HTTP request' and 'Better Logic' apps.

The Humidity, Temperature, and State variables are pushed to and received by Homey as follows:
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Flow%20-%20Homey%20-%20Humidity.png)
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Flow%20-%20Homey%20-%20Temperature.png)
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Flow%20-%20Homey%20-%20State.png)

The flow to start the 'Timer' function in Homey (when humidity is above 60%, and the Itho is not running on the 'Medium' setting, which provides a way to by-pass control by Homey. I use this when taking a bath ;-):
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Flow%20-%20Homey%20-%20Google%20Chrome%202017-02-01%2017.15.10.png)

Homey generates some nice graphs in the 'Insights' interface:
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Insights%20-%20Homey.png)

To be able to graph the State, I assigned each state with a (more or less arbitrary) number:
![alt tag](https://github.com/abaretta/Itho-WIFI-remote-Homey/blob/master/Images/Flow%20-%20Homey%20-%20State%20-%20tracking.png)

OTA updates work with .bin files!

I am not a developer! Use at your own RISK!!

Refer to the original source of the NodeMCU Itho version:
https://www.maredana.nl/itho-mechanical-ventilation-with-esp8266/
