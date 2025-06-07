# Pete's Improved CN3791

## Introduction
Recently I've been building some small, solar-powered [Meshtastic](https://meshtastic.org/) nodes to expand the mesh network coverage in my area. Due to their small size and power efficiency, I have been using [RAK 4631 WisBlock](https://store.rakwireless.com/products/wisblock-meshtastic-starter-kit) systems as the core of these modules.

The WisBlock base boards include a [TP4054](#TP4054) -- a compact (SOT-23-5 sized), linear lithium-ion (Li-ion) charger chip to charge a Li-ion battery connected to the module. Power for the TP4054 can be provided by either a 5V USB connection or a 5V solar panel (or other power source) connected to the board's "SOLAR" input connector.

The TP4054 is fine when powered by USB or some other constant voltage source that can provide (effectively) unlimited current. However, it's not really suited for use with solar because:
1. It has a limited input voltage range (4.5-5.5V).
2. It has a limited charge current (500mA max, configured for 300mA on the RAK board).
3. It is unable to effectively handle an inherently variable, unstable power source like a solar panel.

The ideal choice is a switch-mode battery charger that can adapt its charging current based on the capability of the source to maximize the amount of power produced. These are efficient, generate little heat, and can accept a wide range of input voltages.

The CN3791, made by 

I first considered CN3791 board purchased on the internet (See Figure 1).

<a id="figure1"></a>
[![Generic CN3791 Board](images/CN3791_generic_board-small.jpg)]([images/CN3791_generic_board.jpg])  
*Figure 1: A generic CN3791 board.*