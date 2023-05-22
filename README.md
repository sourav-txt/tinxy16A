# flashing tasmota to tinxy 16A smart switches

Flashing Tasmota to Tinxy 16A switches


tinxy smart switches are pretty cheap switches available for indian customers on amazon and tinxy.in. These switches come with esp8266 chips which can be flashed with tasmota pretty easily

You dont need to cut open the whole package , instead just make a small incision about half a cm away from the esp heatspreader . 
There will be exactly 5 pin holes for soldering. I dont use soldering, instead simply insert male dupoint pins for flashing.

any usb to ttl converter works (CP2102, ftdi or cheap ch340), just connect buttons as 

-----------------------
programmer |    tinxy
-----------------------
vcc        ->   vcc
rx         ->   tx
tx         ->   rx
gnd         ->   gnd
-----------------------

to enter into flash mode, hold push button while powering, this will ensure you are in flash mode.
flash tasmota, then do a power cycle by removing usb and then reinserting it.
now you will be able to see esp AP , connect to this AP and then set up wifi.
then again go to the tasmota home page,

insert following template 

-----------------------------------------------------------------------------------
{"NAME":"Tnxy16A","GPIO":[32,0,0,0,160,224,0,0,288,0,416,0,0,0],"FLAG":0,"BASE":18}
-----------------------------------------------------------------------------------

then go to console and type

-------------------------------------------------------------------------
setoption15 0
setoption68 0
Pwmfrequency 1000
Pwmrange 1023 
pwm1 512

Backlog rule on system#boot do pwm1 512 endon; Rule 1 1

--------------------------------------------------------------------------

This is good enough if you dont need external switch functionality. For external switch functionality , add these to console, this will ensure that by defualt the switch will wait for atleast a about half a second before turning off the relay

-------------------------------------------------------------------------
SwitchDebounce 1009
SwitchMode 1
-------------------------------------------------------------------------

to set timezone to IST,go to console and type

-------------------------------------------------------------------------
Timezone +5:30
-------------------------------------------------------------------------

#this will disable led blinking when mqtt or wifi connection error happens

-------------------------------------------------------------------------
setoption31 1 
-------------------------------------------------------------------------

source : https://templates.blakadder.com/tinxy_1_node_16a.html
