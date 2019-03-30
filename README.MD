JBL Charge 3 SPI pins on mainboard
---------------------------------------


---------------------
Information
---------------------
There are two firmware versions( or more I haven't checked the latest fw), Stock and a newer firmware with Connect+.

Latest firmware provides, customname, remap play button, Connect to Connect+ devices, meanwhile this firmware version adds latency to ADC input, and cutoff noise.
I measured ADC or Line Input whatever you call it with old firmware and new firmware.
Compared both, new firmware adds 21.50ms more latency on ADC input. running both speakers on the same source with just a audio splitter.
When playing very low volume sounds on the analog input, the sound will just.. cutoff.

Disavantages of new firmware:
Loses connection to older devices when in party mode or w/e they call it.
Adds Connect+, basicly broadcast your music and pairs with other devices which is in that mode.
Adds 21.5ms latency on analog input
cut-off threshold is to sensitive.

Stock Old firmware:
Pairs with older devices in Connect.
Doesn't pair with Connect+ devices.
Needs a older version of JBL Connect app to change left/right mode on BT connection.
No custom name on BT. (however you can change that in PSTOOL!)

------------------------
Why?
------------------------
I might missing some features or information isn't right that I typed here above, > correct me if im wrong.
Sofar my purpose to downgrade my JBL Charge 3 was purely to use two of them on analog input, connected to my pc and having the lowest latency as possible because there is a DSP inside that takes the signal and corrects the EQ curve on these drivers.
I just ran into a few issue after I updated the JBL Charge 3, as JBL Connect said it was not possible to downgrade, well it is now, through SPI, and having a not updated device to dump the firmware off from it.

------------------------
Instructions
------------------------
Well I'm not a tutorial guy, you can find the dump files in this github.
Use BlueFlash to backup your current firmware, Dump twice! and compare them to ensure the dump is successful.
After you are connected, besure you connected USB power to the device! then press stop processor. (if you did not connected USB power, it will cut off power to the module since the module switches the internal psu).
Dump, then upload the new fw, download, verify, then start processor, then you press the power button on the jbl. should boot up!

I was using an Arduino board, disconnected the microprocessor and using the FT232RL only. you might need to solder pin 3 (RTS) on the ft chip with a thin wire. and desolder pin 4 and connect this to 3v3 volt. (thus it is normally operating on 5v because arduino)
Connect all pins thru a 220/330ohm resistor. and use the pin layout provided here.


JBL board | FT232
----------|-------
1 GND   	| GND
2 MISO   	| DSR
3 MOSI   	| RI#
4 CLK    	| RTS
5 CSB    	| DTR
6 3v3    	| leave unconnected

There are no markings unlike the flip4 hack from https://hackaday.io/project/162337/instructions
I figured it out by just guesing and if it was not working i just swap pins until the LED's starts to flash rappidly. I was running the BlueTest3 software since it was retrying connection until it connects.

As for the programmer/driver install, please follow https://github.com/lorf/csr-spi-ftdi
It is not really necesery to update the config file (on PSTOOL), but if you do, besure to preserve the mac address of that device!

![alt text](https://github.com/Dnstje/JBL-Charge-3-firmware/blob/master/APL05732.JPG)
![alt text](https://github.com/Dnstje/JBL-Charge-3-firmware/blob/master/APL05738.JPG)
