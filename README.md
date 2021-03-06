# grbl-polar

***
Graffiti robot firmware base on [Grbl v0.9](https://github.com/grbl/grbl)

The implemented kinematics allow a 2 string + gravity system (as in [hektor](http://juerglehni.com/works/hektor)), and the pwm support allows triggering the spray using a servo-motor.

additional features:
  * define POLAR: swaps from cartesian to polar kinematics. It's required to set up the distance between the motors. Homing at startup is essential, otherwisse positioning can not be achieved.
  * define RC_SERVO: Use PIN D11 to drive the servo. Use the commands M03 Sxxx (xxx between 0 and 255) to rotate the servo between 0-180. The command M05 turns the servo to zero degrees. [source](https://github.com/robottini/grbl-servo)
  
  
![alt text](https://github.com/ilaro-org/grbl-polar/blob/master/v0.jpg "first test at hangar.org")


##Flashing

To flash the grbl to arduino we did it through terminal. To compile the code:   
    
    make clean
    make grbl.hex

And to flash it:   
    
    (AVRDUDE-PATH)/avrdude -C(AVRDUDE.CONF-PATH)/avrdude.conf -v -patmega328p -carduino -P/dev/(USB) -b(BAUTRATE) -D -Uflash:w:(GRBLPOLAR-PATH)/grbl.hex:i
   
e.g:   
    
    /home/Applications/arduino/hardware/tools/avr/bin/avrdude -C/home/Applications/arduino/hardware/tools/avr/etc/avrdude.conf -v -patmega328p -carduino -P/dev/ttyUSB0 -b57600 -D -Uflash:w:/POLAR/grbl-polar/grbl.hex:i 


##Configuring Grbl-polar
The Grbl-polar's configuration is the same as in [Grbl v0.9] (https://github.com/ilaro-org/grbl-polar/wiki/Configuring-Grbl-v0.9). But we have added a new setting: 'distance'. You can define it through the GUI settings or by the command line:   

     $27=1000 (distance, mm)

It defines the distance between the two motors and it is needed in order to achieve machine's positioning.

![alt text](https://github.com/ilaro-org/grbl-polar/blob/master/grbl-polar.JPG)

##Gcode

To generate the G-code you can use any slicing program and slice a vectorial drawing. We used Inkscape because it is opensource and you can do vectorial drawings and slice them directly with the [Laser Plug-In](https://jtechphotonics.com/?page_id=2012). You have to take into account when sittuating the drawing in the page that the center (0,0) of the robot is situated on the left motor.

To send G-code to the robot we had used http://chilipeppr.com/grbl or [Universal G-code Sender](https://github.com/winder/Universal-G-Code-Sender)



GPLv3 license
