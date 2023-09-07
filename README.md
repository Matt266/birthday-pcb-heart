# PCB Heart As Birthday Present

As birthday present for our mother my brother and I decided to create a heart-shaped PCB with a buzzer
to play "happy birthday" and LEDs to look pretty. It also should be powered by battery.

Two buttons allow cycling through brightness levels and to initiate the "happy birthday".  

<br><img align="center" width=500 height=auto src="Herz_Platine.jpg" alt="finished PCB" title="finished PCB"><br>


## The Circuit

The exact partnumbers can be taken from the bom and the KiCAD project. I decided to make use of a LiPo-battery for
the lower self discharge, higher capacity and possibility to recharge in comparison to regular batteries. 

A battery management ic controls charging and allowed me to add a usb connector as charging port. The PCB is also 
powered during charging. A P-Channel MOSFET protects the circuit for reverse polarity on the LiPo-Input. 

Two charge pumps step up the voltage to 5V. This made it Arduino compatible so I could more easily use an Arduino as
in circuit programmer. Also it kept the circuit smaller than inductor based boost-converter. This helped fitting all
components within the heart shape. 

The LEDs and the buzzer are controlled via N-Channel MOSFETs (one for all LEDs one for the buzzer) and connected to
PWM capable pins on the MCU.

To make it more Arduino capable and therefore ease programming for my brother I chose the classic Atmega328p as MCU. 
It was his first time programming something embedded and he did a great job! :)

## The Software

The Software was completely written by my brother (TODO: add Sketch to this repo).


## The Problems

As with all projetcs there are some things that I could have done better in the hindsight.

First of all I didn't include a switch on the PCB. I added one external switch between the LiPO-battery
and PCB afterwards but that isn't nearly as comfortable as having it included directly on the PCB.

The second problem are the charge pumps. While they get the job done they heave a massive quiescent current
and aren't really efficient.  Also running the MCU from a 5V supply voltage increased its power consumption in comparison to e.g. 3.3V.
As the voltage is stepped up the current drawn from the battery inceases even further.
This combination is responsble for a large standby current of 50mA. This massive quiescent current even makes it
unnecessary to consider putting the MCU sleeping. The current draw would remain high nonetheless.
