# Pete's Improved CN3791

## Introduction
I wanted a small, efficient, switch-mode, MPPT lithium-ion charger for some of my solar-powered [Meshtastic](https://www.meshtastic.org/) nodes and found the CN3791, made by [Shanghai Consonance](http://www.consonance-elec.com/en/), which seemed to fit the bill.

Various online vendors sell a common CN3791 board that looks like this:

[![Generic CN3791 Board](images/CN3791_generic_board-small.jpg)](images/CN3791_generic_board.jpg)  

However, I don't like these boards for several reasons:
1. The Maximum Power Point voltage is set by R1 and R2, which form a voltage divider between Vin and GND, with the midpoint going to the chip's MPPT pin. These come set from the factory with several options for nominal input voltages (5V, 6V, 9V, and 12V) and cannot be set or adjusted by the user except by replacing tiny 0603 resistors.
2. The layout is horrendous, and doesn't follow [good layout design](files/rohm-buck-converter-application-note.pdf) for buck converters (or even the layout recommendations in the [datasheet](files/Datasheet_CN3791.pdf)). Specifically:
    1. The capacitors are really far from the switching MOSFET at the top making the AC current loop needlessly large.
	2. It uses a big electrolytic capacitor, but no ceramic capacitor on the input. I dislike using electrolytics due to their aging in hot environments, like a rooftop enclosure roasting in the sun. Also, C3 and R4 are for loop compensation, and C2 is for the internal power supply for the P-channel MOSFET driver. C2 and C3 aren't decoupling capacitors.
	3. It has no reverse polarity protection on the input, which could result in the board being damaged if the input is connected in reverse, as well as letting the battery potentially discharge through a solar panel at night if the panel doesn't have a blocking diode (many small ones don't).
	4. The output capacitors don't follow the datasheet's recommendation (or good practice) to be connected to the same copper as the input capacitors before tying into the system ground.
	5. It uses a tantalum output capacitor. I prefer ceramic capacitors since "bursting into flame" is not one of their failure modes.
	6. It has parallel input and output connectors for no apparent reason.