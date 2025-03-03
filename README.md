# Intro

This module adds touch based solder functionality to the awgem sj1 soldering iron, so that the tip only heats set temperature, when the iron is picked up by hand (using a capacitive touch sensor), and cuts power to the tip otherwise. 

## Visual Overview

<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/d439c486-e7ef-4c7e-a49f-96161c766972" alt="PCB Top View"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/fa55ac4c-7db0-4c4f-807e-2184be637fd4" alt="PCB Bottom View"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/d439c486-e7ef-4c7e-a49f-96161c766972" alt="Physical top"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/d439c486-e7ef-4c7e-a49f-96161c766972" alt="Physical assembled top"/>
    </td>
  </tr>
</table>

## Key Features

- **Add-on**: The PCB is made to overlay on the original one and mounted by solder spots, together with their connections.
- **Direct connections**: The pins on the pcb directly connect to the function points that it needs to function properly.
- **Minimal modification**: The iron's pcb needs minimal modification, like removal of a mosfet

## Installation

### On SJ1 mainboard

- Pull out the mainboard from its housing (buttons will fall off)
- Cover the display with e.g. capton tape
- Remove the power mosfet (Q1) from the SJ1 pcb
- Cover the removed mosfet's pads with capton tape
- Flatten the tip holding pads, by removing solder (only on the side of the pcb, where the mosfet was)
- Pre-tin the 2 nearest round pads to the power mosfet

### On touch mod pcb

- Clean up the edges by filing the trace/pad excess away
- Solder on the components listed in the BOM below, except for the SOP8 mosfet (AO4413)
- Solder a nickel strip on the big pad, creading a surface to touch the metal cap
- Place the touch module on the SJ1 pcb
- While squeezing the pcb's together, solder the pads on, reducing any gap between the pcb's
- Solder the SJ1'S 472 smd resistor's top to the touch module's aligned pad
- Below JMP1, solder the round pad (=3V3 input) to the SJ1's VDD with a wire
- Left to the bottom Hole, solder the round pad (= GND) to the SJ1's GND with a wire
- Solder on the SOP8 Mosfet (AO4413)
- Remove tape from display
- Reassemble the soldering iron & press the buttons back in

### Optimal Iron Settings

For a safe and convenient workflow with minimal interaction:  

- **Auto Sleep: On (e.g., 600s)**  
  - Turns the tip off after 10 minutes of inactivity.  
  - Reheats when motion is detected (e.g., picking up the iron).  
  - Only heats while being touched, reducing fire risk.

## BOM

The parts are listed in the recommended order of soldering.
Note on C1: 
- Use 22pF, if only the silver part of the handle should react
- Use 10pF, if the whole metal body should react

| Reference | Part Name               | Description                           |
|-----------|-------------------------|---------------------------------------|
| U2        | TTP223-BA6              | Touch capacitive IC, SOT23-6 package  |
| JP2       | Jumper pad              | Short to enable led                   |
| C1        | 0603-0-50pF             | Capacitor, 0603 sized, 0 to 50 pico Farads (adjust for touch sensibility) |
| D1        | RGB Led                 | Led with common VCC, 3528 sized       |
| R1        | 0603-1k                 | Resistor, 0603 sized, 1 kilo Ohm                  |
| R2        | 0603-1k                 | Resistor, 0603 sized, 1 kilo Ohm      |
| U4        | AO3400                  | N-ch Mosfet, SOT23-3 package          |
| R5        | 0603-10k                | Reisitor, 0603 sized, 10 kilo Ohm     |
| JP1       | Jumper pad              | Short to enable touch controlled mosfet gate |
| R3        | 0603-10k                | Reisitor, 0603 sized, 10 kilo Ohm     |
| R4        | 0603-10k                | Resistor, 0603 sized, 10 kilo Ohm
| T1        | S8550                   | PNP Transistor, SOT23-3 package       |
| BIG_PAD   | -                       | Touch interface, solder nickel strip on this |
| U1        | AO4413                  | P-ch Mosfet, SOP8 package             |

## Key Takeaways

- Tip controlling mosfet (now called pmos) gate is pulled up to PD VCC (e.g. 12V or 20V) with a 472 labelled smd resistor
- The gate of the pmos should never be left floating, else the tip will heat into oblivion and the pmos will overheat and break
- The gate of pmos is grounded by a transistor to control the power flowing to the tip from source to drain, with a 16 kHz pwm signal, where the transistors output duty cycle controls the temperature
- The TTP223 IC MUST be BA6 variant, as that is the only one without a timeout. Other TTP223 IC's have a 10 second timout, so they output low after 10 seconds, even while being touched

## Demo

https://github.com/user-attachments/assets/4df80c9a-d933-4be5-8bb9-def0f2be151d
