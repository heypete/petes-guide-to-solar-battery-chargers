# Pete's Guide to Solar Li-Ion Battery Charger Chips & Circuits

## Introduction
Recently I've been building some small, solar-powered [Meshtastic](https://meshtastic.org/) nodes to expand the mesh network coverage in my area. Due to their small size and power efficiency, I have been using [RAK 4631 WisBlock](https://store.rakwireless.com/products/wisblock-meshtastic-starter-kit) systems as the core of these modules.

The WisBlock base boards include a [TP4054](#TP4054) -- a compact (SOT-23-5 sized), linear lithium-ion (Li-Ion) charger chip to charge a Li-Ion battery connected to the module. Power for the TP4054 can be provided by either a 5V USB connection or a 5V solar panel (or other power source) connected to the board's "SOLAR" input connector.

While I'll discuss the [TP4054 in more detail later](#TP4054), I wanted to mention that I like it in its intended role as a USB-powered battery charger and will briefly list its shortcomings when connected to a solar panel:
1. It has a limited input voltage range (4.5-5.5V).
2. It has a limited charge current (500mA max, configured for 300mA on the RAK board).
3. It is unable to effectively handle an inherently variable, unstable power source like a solar panel.

These shortcomings led me to investigate alternative chargers and create this page. I hope you find it useful.

***
## Technical Background
### Li-Ion Batteries
[Lithium-ion batteries](https://en.wikipedia.org/wiki/Lithium-ion_battery) have many desirable properties that make them useful for powering electronics:
1. They provide a convenient voltage (nominally 3.7V, up to 4.2V).
2. They do not exhibit any memory effect, unlike other battery chemistries.
3. Their charging requirements are fairly reasonable [(constant-current/constant voltage)](#constant-current/constant-voltage-charging)

#### Charging Requirements
##### Constant Current/Constant Voltage Charging
##### Charge Termination
### Battery Protection
#### Battery Overdischarge Voltage Considerations
#### DW01A
2.5V  

User-specified current limit, depending on external mosfet. 

~3A for 8205A.

$0.035 ($0.70/20) for DW01A

$0.0405 ($0.41/10) for 8205A.
#### XB8089D0
2.9V

10A

$ 0.15 (0.77/5)
#### XB5358D0
2.9V

3.3A

$0.17 ($0.86/5)
### Solar Panels
#### Constant Current vs. Variable Current
### Linear vs. MPPT
#### Linear Charging
#### Maximum Power Point Tracking

***
### Linear Chargers
#### TP4054
$0.022 ($0.45/20)

4.5V-5.5V

500mA max.

#### TP4056
#### CN3065
#### CN3163

***
### Switching Chargers
#### "MPPT" Chargers
###### CN3791

#### True MPPT Chargers

***
## Testing and Comparison of Chargers
### Test Methods
### Test Results