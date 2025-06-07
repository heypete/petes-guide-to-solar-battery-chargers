# Pete's Improved CN3791

## Introduction
I wanted a small, efficient, switch-mode, MPPT lithium-ion charger for some of my solar-powered [Meshtastic](https://www.meshtastic.org/) nodes and found the CN3791, made by [Shanghai Consonance](http://www.consonance-elec.com/en/), which seemed to fit the bill.

Various online vendors sell a common CN3791 board that looks like this:

[![Generic CN3791 Board](images/CN3791_generic_board-small.jpg)](images/CN3791_generic_board.jpg)  

However, I don't like these boards for several reasons:
1. The Maximum Power Point voltage is set by R1 and R2, which form a voltage divider between Vin and GND, with the midpoint going to the chip's MPPT pin. These come set from the factory with several options for nominal input voltages (5V, 6V, 9V, and 12V) and cannot be set or adjusted by the user except by replacing tiny 0603 resistors.
2. The layout is horrendous, and doesn't follow [good layout design](files/rohm-buck-converter-application-note.pdf) for buck converters (or even the layout recommendations in the [datasheet](files/Datasheet_CN3791.pdf)). Specifically:
    1. The capacitors are really far from the switching MOSFET at the top making the AC current loop needlessly large.
	2. It uses a big electrolytic capacitor, but no ceramic capacitor on the input. I dislike using electrolytics due to their aging in hot environments, like a rooftop enclosure roasting in the sun. Also, C3 and R4 are for loop compensation, and C2 is for the internal power supply for the P-channel MOSFET driver. C2 and C3 aren't decoupling capacitors.
	3. It has no reverse polarity protection on the input, which could result in the board being damaged if the input is connected in reverse, as well as letting the battery potentially discharge through a solar panel at night if the panel doesn't have a blocking diode (many small ones don't).
	4. The output capacitors don't follow the datasheet's recommendation (or good practice) to be connected to the same copper as the input capacitors before tying into the system ground.
	5. It uses a tantalum output capacitor. I prefer ceramic capacitors since "bursting into flame" is not one of their failure modes.
	6. It has unprotected parallel input and output connectors for no apparent reason.
	7. The load would presumably be attached to the battery (or the second BAT connector). The load current would be added to the charge current going through the current sense resistor, which would interfere with charge termination.
	8. They have no mounting holes.
	9. The 50 ohm current sense resistor sets a charge limit of 2.4A.

Therefore, I set out to design my own.

## Pete's Improved CN3791 Board
### Basic Design Principles
I wanted my board to fulfil the following requirements:
1. Be compact in size, ideally around 2" (~5.1 cm) long and 1" (~2.5 cm) wide.
2. Have reverse polarity protection on the input, protecting against incorrectly connected solar panels and reverse current flow at night.
3. Use [good layout design](files/rohm-buck-converter-application-note.pdf).
4. Use only ceramic capacitors.
5. Have 2 mm mounting holes.
6. Be able to accept input voltages up to around 25V DC.
7. Be modular to allow several design variants, namely:
    1. A "core" that includes the key power supply elements, connectors, etc. but nothing else.
	2. A variant with a [DW01A](https://www.best-microcontroller-projects.com/dw01a.html) battery protection chip, for those who want to maximize the energy they can get out of their battery by having a low-voltage cut-off limit of 2.5V.
	3. A variant with a battery protection chip with a higher cut-off voltage to play nice with RAK Wireless Meshtastaic nodes; some people have reported "brownout" issues when the battery voltage gets too low. I ended up making two variants, one with a [XB8089D0](files/Datasheet_XB8089D0.pdf) (10A overcurrent limit) and one with a [XB5358D0](files/Datasheet_XB5358D0.pdf) (3.3A overcurrent limit). Both have a low-voltage cut-off limit of 2.9V, which is perfect.
8. Allow for user-adjustable MPP voltage.
9. Allow for user-adjustable maximum charge current.

As of this writing, I've designed variants that fulfil items #1-8, and intend to add #9 in the near future.