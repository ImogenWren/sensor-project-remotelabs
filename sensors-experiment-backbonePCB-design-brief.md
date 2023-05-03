# Sensors One - Backbone PCB - Power Supply 

## Description
The backbone PCB will provide all power requirements to the sensors 1 experiment. It will manage routing the PicoScope probes to defined pins on the backbone header, which will join the backbone PCB to the sensors one experiment PCB

## Power Requirements

### Sensors Experiment
- Bi-polar supply for Op-Amps and similar (100mA per 5v rail (+-))
- Power for Fan (60mA @ 12v) - needs to be 5v
- Power for Bulb. (~60mA @ ~5v)
https://www.switchelectronics.co.uk/6v-60ma-miniature-e10-mes-lamp-bulb
- Embedded MCU (200mA max @ 5v)
- 

Backbone PCB must provide the following power outputs:

- (+-)5v - to sensors experiment (100mA per rail? is this enough for a fan and lightbulb)
- +5v for SBC. 3A specified.
- +5v for microcontroller/arduino (200mA Max)
- analog switch power requirements?
- any other board level hardware

## Power Distribution
- (+-)5v will be provided using linear power regulators or similar.
- +5v for SBC will be provided via a buck converter capable of 3A output @ 5v 
	- #TODO Design decision, adjustable buck or not? adjustable means power for odroid easy to set
- +5v for Arduino will be provided by another linear regulator
	

## Power Distro Parts Specification

### Option Q +-5v Regulator
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

Assuming 24VDC input and 200mA output = 5x0.2 = 1W, with efficiency this means

50mA @ 24v

### +5v Regulator

### -5v Regulator

#### Option A LDO
- JLCpart: C358376
Datasheet
https://datasheet.lcsc.com/lcsc/1912111437_Foshan-Blue-Rocket-Elec-79D05_C358376.pdf

Specs:
- Vout = 
- Vdropout =  1.4v
- Package = TO-252-2
- Vin(max) = ? -35 compared to output? so 30v? or -30v? real unclear. datasheet little help-
- Vin(min) = Vout +(-) Vdropout = -6.4v or 6.4v?

#### Option B Linear Regulator

- JLCpart: 
Datasheet
https://www.datasheetq.com/LM79XXCT-doc-Fairchild

Specs:
Vout =
- Vdropout =  1.4v
- Package = TO-252-2
- Vin(max) = ? -35 compared to output? so 30v? or -30v? real unclear. datasheet little help-
- Vin(min) = Vout +(-) Vdropout = -6.4v or 6.4v?


### Negative Buck Converter?
https://www.vishay.com/docs/76946/creatingnegativeoutputvoltage.pdf

### Positive Buck Converter for SBC
- Same as ISOpower board

Vin: 24VDC
Vout: 5vDC
Iout: 3A
Pout: 15W
Efficiency ~ 0.80
Pmax = Pout/0.80 = 18.75W
Iin =  18.75/24 = 0.78125 A 780.125mA

	
## Power Input Requirements
For Sensors experiment:
- 50mA max @ 24v
For SBC
- 800mA max @ 24v
