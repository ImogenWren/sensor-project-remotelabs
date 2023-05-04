# Sensors One - sensors-backbone-pcb - Power Supply 

## Description
The backbone PCB will provide all power requirements to the sensors One experiment. It will manage routing the PicoScope probes to defined pins on the backbone header, which will join the backbone PCB to the sensors one experiment PCB. This document outlines the power distribution section of the system, and will define the requirements for power supplied to the sensors-backbone-pcb.

## Power Requirements

### Sensors Experiment Power Requirements
_All power requirements for the **sensors-one-pcb** must be provided by **sensors-backbone-pcb**_

#### Bi-polar Op-Amp Supply
- Bi-polar supply for Op-Amps and similar (100mA per 5v rail (+-)? is this enough)
#### 5v Fan
- Power for Fan (?mA @ 5v) PWM Capable
	- Fan Option A: Cheap but no data
		- https://www.unmannedtechshop.co.uk/product/40mm-cooling-fan-5v-pwm-adjustable/
	- Fan Option B: Expensive but has whitepaper with full specifications:
		- 0.35 W
		- 70 mA @ 5v
		- https://www.quietpc.com/nf-a4x10-5v-pwm
		- https://noctua.at/pub/media/wysiwyg/Noctua_PWM_specifications_white_paper.pdf
		- Also have a 2 pulse per revolution output that can be used to sense RPM
#### Torch Bulb
- Power for Bulb. (~60mA @ ~5v)
	- 	https://www.switchelectronics.co.uk/6v-60ma-miniature-e10-mes-lamp-bulb

#### Additional Power Requirements
- #TODO: Any MCU required on experiment board?



## SUMMARY: sensors-one-pcb power Requirements
- Bi-Polar (+-)5v DC up to 100mA each rail
- High Current 5v (At least 200mA)


### Backbone PCB Power Requirements
_Power Requirements for all hardware on **sensors-backbone-pcb**
- Embedded MCU (200mA max @ 5v)
- analog switch power requirements
	- Quiecient current ~ 6 uA 
	- Assume that this is within spec for MCU
- any other board level hardware
- +5v for SBC. 3A specified.


## Power Distribution - sensors-backbone-pcb
_Detail suitable options for providing for each of the power requirements_

### To Sensors One
-(+-)5v will be provided using linear or switching power regulators or similar.
- +5v High Current will be provided using regulator or buck converter
### For Local Use
- +5v for SBC will be provided via a buck converter capable of 3A output @ 5v 
- +5v for Embedded Systems provided by Buck Converter or Regulator (Could this be shared with sensors 1 high current?)
	

## Power Distro Parts Specification
_Specify specific solutions for each power requirement_

### Bi-Polar Power Supply

#### (+-5v) Bi-Polar Supply for sensors-one-pcb - OPTION A
https://uk.rs-online.com/web/p/dc-dc-converters/1227021
https://docs.rs-online.com/2f4c/0900766b8154511b.pdf
Specs:
- Vout 			= +-5v 
- Power Rating 	= 1W
- Iout(max) 	= 200mA (100mA per output)
- Vdropout		= n/a
- Package 		= SIP
- Vin(min)	 	= 4.5  (check datasheet - 12v and 24VDC in models available
- Vin(max) 		= 5.5 
- Efficiency 	= 83%
- Cost			= £4.01
- Inoload		= 20mA
Assuming 24VDC input and 200mA output = 5x0.2 = 1W, with efficiency this means: 50mA @ 24v

If this power supply is too small then ->

###  Option D Negative Buck Converter
https://www.vishay.com/docs/76946/creatingnegativeoutputvoltage.pdf

### High Current 5v supply

#### Buck Converter
- Same as ISOpower board

Vin: 24VDC
Vout: 5vDC
Iout: 3A
Pout: 15W
Efficiency ~ 0.80
Pmax = Pout/0.80 = 18.75W
Iin =  18.75/24 = 0.78125 A 780.125 mA

#### Switching Regulator
- Same as supervisor PCB

https://recom-power.com/pdf/Innoline/R-78C-1.0.pdf

Vin: 7 - 42 (24v)
Vout: 5 vDC
Iout: 1 A
Pout: 5 W
Efficiency  0.85
Pmax = Pout/0.85 = 6 W
Iin =  6/24 = 0.25 A 250 mA


### SBC Power Supply

#### (+5v) Buck Converter for SBC
- Same as ISOpower board

Vin: 24VDC
Vout: 5vDC
Iout: 3A
Pout: 15W
Efficiency ~ 0.80
Pmax = Pout/0.80 = 18.75W
Iin =  18.75/24 = 0.78125 A 780.125 mA

### Embedded MCU and Associated circuits (inc switches)
Any reason to keep this seperate from the high current supply - Especially if using buck converter?

Assuming that it is seperate just for Max Current Calculations





	
## Power Input Requirements to sensor-backbone-pcb
_Ensure that all specified hardware can be provided +24v, and calculate *Itotal* for 24v input_

For sensors-one-pcb:
- Bi-Polar Supply 
	- 50mA max @ 24v
- High Current (using worse case scenario):
	- 800mA @ 24v
For Embedded System sensors-backbone-pcb:
	- 800mA @ 24v
For SBC
	- 800mA max @ 24v

## Total Power Requirement for sensors-backbone-pcb
 2.5 A @ 24 V
 
 Design spec for 3 A
