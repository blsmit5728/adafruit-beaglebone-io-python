## Adafruit's BeagleBone IO Python Library

This is a set of Python tools to allow GPIO, PWM, and ADC (coming soon) access on the BeagleBone using the Linux 3.8 Kernel and above (latest releases).

It has been tested on the 5-20 and 6-6 Angstrom image on the BeagleBone Black.

## Installation

    git clone git://github.com/adafruit/adafruit-beaglebone-io-python.git
    #set the date and time
    /usr/bin/ntpdate -b -s -u pool.ntp.org
    #install dependency
    opkg update && opkg install python-distutils
    cd adafruit-beaglebone-io-python
    python setup.py install

## Usage

Using the library is very similar to the excellent RPi.GPIO library used on the Raspberry Pi.  Below are some examples.

#### GPIO Setup
Import the library, and setup as GPIO.OUT or GPIO.IN

    import BBIO.GPIO as GPIO

    GPIO.setup("P8_14", GPIO.OUT)
    
You can also refer to the pin names:

    GPIO.setup("GPIO0_26", GPIO.OUT)

#### GPIO Output
Setup the pin for output, and write GPIO.HIGH or GPIO.LOW.  Or you can use 1 or 0.

    import BBIO.GPIO as GPIO

    GPIO.setup("P8_14", GPIO.OUT)
    GPIO.output("P8_14", GPIO.HIGH)

#### GPIO Input
Inputs work similarly to outputs.

    import BBIO.GPIO as GPIO

    GPIO.setup("P8_14", GPIO.IN)
    
Polling inputs:
    
    if GPIO.input("P8_14"):
        print("HIGH")
    else:
        print("LOW")

Waiting for an edge (GPIO.RISING, GPIO.FALLING, or GPIO.BOTH:

    GPIO.wait_for_edge(channel, GPIO.RISING)
    
Detecting events:

    GPIO.add_event_detect("P9_12", GPIO.FALLING)
    #your amazing code here
    #detect wherever:
    if GPIO.event_detected("P9_12"):
        print "event detected!"

#### PWM
        
    import BBIO.PWM as PWM
    #PWM.start(channel, duty, freq=2000)
    #duty values are valid 0-100
    PWM.start("P9_14", 50)
    
    PWM.set_duty_cycle("P9_14", 25.5)
    PWM.set_frequency("P9_14", 10)
    
    PWM.disable("P9_14")
    PWM.cleanup()
        
## Running tests

Install py.test to run the tests.  You'll also need the python compiler package for py.test.
  
    opkg update && opkg install python-compiler
    #Either pip or easy_install
    pip install -U pytest
    easy_install -U pytest

Execute the following in the root of the project:

    py.test

## Credits

The BeagleBone IO Python library was originally forked from the excellent MIT Licensed [RPi.GPIO](https://code.google.com/p/raspberry-gpio-python) library written by Ben Croston.

## License

Written by Justin Cooper, Adafruit Industries. BeagleBone IO Python library is released under the MIT License.
