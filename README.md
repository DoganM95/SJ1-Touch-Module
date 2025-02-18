# Intro

This module adds touch based solder functionality to the awgem sj1 soldering iron, so that the tip only heats set temperature, when the iron is picked up by hand (using a capacitive touch sensor), and cuts power to the tip otherwise. 

## Visual Overview

<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/62e08359-938f-40d9-85d9-e77fa0acb89b" alt="PCB Top View"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/fe99fc65-409d-49a7-9eb0-98ec5676bbdd" alt="PCB Bottom View"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/62e08359-938f-40d9-85d9-e77fa0acb89b" alt="Physical top"/>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/62e08359-938f-40d9-85d9-e77fa0acb89b" alt="Physical assembled top"/>
    </td>
  </tr>
</table>

## Key Features

- **Add-on**: The PCB is made to overlay on the original one and mounted by solder spots, together with their connections.
- **Direct connections**: The pins on the pcb directly connect to the function points that it needs to function properly.

## Preparation

### On SJ1 mainboard

- Cover the display with e.g. capton tape to prevent scratches during installation
- Remove the power mosfet (Q1) from the SJ1 pcb
- Remove solder until the tip-holding pads are flat on the side, where the mosfet is
- Cover the mosfet pads with captop tape, so it does not touch the gate pin of the touch module that will sit on it
- Pre-tin the 2 nearest round pads to the power mosfet with a blow of solder

### On touch mod pcb

- Clean up the via's by filing the trace/pad excess away
- Solder on the components listed in the BOM, except for the SOP8 mosfet (AO4413)
- Solder a nickel stripe on the big pad, creading a surface to touch the metal cap
- Place the touch module on the SJ1 pcb, positioning it correctly with pads matching the holes
- While squeezing the pcb's together, solder the pads on, one after another, reducing any gap between the pcb's
- Solder the 472 smd resistor's top to the touch module's aligned pad
- Below JMP1, solder the round pad (=3V3 input) to the SJ1's VDD with a wire
- Left to the bottomHole, solder the round pad (= GND) to the SJ1's GND with a wire
- Solder on the SOP8 Mosfet (AO4413)

## BOM

The parts are listed in the recommended order of soldering.

| Reference | Part Name               | Description                           |
|-----------|-------------------------|---------------------------------------|
| U2        | TTP223                  | Touch capacitive IC, SOT23-6 package  |
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
