# Intro

This module adds touch based solder functionality to the awgem sj1 soldering iron, so that the tip only heats set temperature, when the iron is picked up by hand (using a capacitive touch sensor), and cuts power to the tip otherwise. 

## Visual Overview

<table>
  <tr>
    <td>
      <img src="" alt="PCB Top View"/>
    </td>
    <td>
      <img src="" alt="PCB Bottom View"/>
    </td>
    <td>
      <img src="" alt="PCBWay order raw"/>
    </td>
    <td>
      <img src="" alt="PCBWay order assembled"/>
    </td>
  </tr>
</table>

## Key Features

- **Add-on**: The PCB is made to overlay on the original one and mounted by solder spots, together with their connections.
- **Direct connections**: The pins on the pcb directly connect to the function points that it needs to function properly.

## BOM

The parts are listed in the recommended order of soldering.

| Reference | Part Name               | Description                           |
|-----------|-------------------------|---------------------------------------|
| U2        | TTP223                  | Touch capacitive IC, SOT23-6 package  |
| D1        | RGB Led                 | Led with common VCC, 3528 sized       |
| C1        | 0603-0-50pF             | Capacitor, 0603 sized, 0 to 50 pico Farads (adjust for touch sensibility) |
| R2        | 0603-5.1k               | Resistor, 0603 sized, 5.1 kilo Ohm    |
| C1        | 0603-100nF              | Capacitor, 0603 sized, 100 nano Farad |
| C2        | 0603-4.7uF              | Capacitor, 0603 sized, 4.7 micro Farad |
| JP1       | Jumper                  | short: mid (VCC) with left/inner (3V3) or right/outer (5V)|
| U4        | AO3400                  | N-Channel Mosfet, SOT-23 package      |
| U3        | AO3400                  | N-Channel Mosfet, SOT-23 package      |
| U1        | AMS1117 3.3V            | 5V to 3.3V Voltage regulator, SOT-223 package |

## Key Takeaways

- Tip controlling mosfet (now called pmos) gate is pulled up to PD VCC (e.g. 12V or 20V) with a 472 labelled smd resistor
- The gate of the pmos should never be left floating, else the tip will heat into oblivion
- The gate of pmos is grounded to control the power flowing to the tip from source to drain, with a 16 kHz pwm signal, where its duty cycle controls the temperature
