# radio2serial

* radio2serial.ino
* version: 0.5
* github url: http://smarturl.it/radio2serial
* Author : Sarrailh Rémi
* Libraries Author : fuzzilogic/airspayce/fastled

#Description
An autonomous arduino radio 433Mhz transceiver.
As long as you can use **USB serial**, it will works with it (**pc/android/embedded**).

It will automatically check if your receiver/transmitter are correctly plugged on started up.

LED ERROR CODE (still)
- Blue : Text too long
- Red : Transmitter not detected
- Yellow : Receiver not detected

LED INFO CODE (blink)
- Blue : Old code sent
- Green : New code sent / Test Radio Tx
- Yellow : text code sent / Boot

# Protocols managed:
* RemoteTransmitter (old)
* NewRemoteTransmitter (new)
* RadioHead (text)

See https://bitbucket.org/fuzzillogic/433mhzforarduino/ for more information.

# Library required
* RadioHead : http://www.airspayce.com/mikem/arduino/RadioHead/
* 433mhzforarduino : https://bitbucket.org/fuzzillogic/433mhzforarduino/
* FastLed : http://fastled.io/

# PinOut
Everything can be changed except for Receiver.
* ASK 433Mhz Transmitter                : ```` 10````
* ASK 433Mhz Receiver (RXB6 recommanded): ```` 2````
* Neopixel (WS2812b)                    : ```` 4````

# Usage
* Commands are sent with a REST syntax
````/radio/text/Hello World````  
* Data are received in JSON
````{"data" : "/radio/text/Hello World"}````
* Errors are received in JSON
```` {"err":"Rx not plugged"} ````
* Debug info are received in JSON
```` {\"ret\":\"/radio/OK\"} ````


Here is some examples of usage
Type into your arduino serial port theses messages to use them

## info
Display sketch name/url/version/pinout and state.
````  info ````
***return***
```` {"file":"radio2serial.ino","url":"smarturl.it/radio2serial","ver":"0.50","pins":"tx:10;rx:2;led:4","state":"tx:1;rx:1"} ````
## radio
.
Turn on chacon switch with address 1234 and unit code 0
```` /radio/new/1234/0/on ````

Turn off chacon switch with address 1234 and unit code 0  
```` /radio/new/1234/0/off ````  

Dim chacon switch with address 1234 and unit code 0 to level 5
```` /radio/new/1234/0/5 ````

Send ON with old code
```` /radio/old/1234 ````

You can add pulse into your new/old
``` /radio/old/1234/400 ```
``` /radio/new/1234/0/off/260 ```

## led
blink the led in green  
```` /led/green ````

Display color availables   
```` /led/? ````
