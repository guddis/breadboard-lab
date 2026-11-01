# The Pocket Adder

Four switches, three logic chips, and a circuit that knows how to add.

You dial two binary numbers on four switches — anything from 0 to 3 each — and three lamps
light up with the arithmetic sum, from 0 to 6. There is no microcontroller, no code, and no
calculator chip. The addition is done entirely by nine discrete logic gates wired into half
adders and a full adder, just as Claude Shannon first proved in 1937.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/pocket-adder/guide.html) in a browser** — that's the real guide, with diagrams and
a working simulator you can play with before touching a wire. This file is the bench
reference: parts, wire lists, pinouts, and troubleshooting.

Build [the Gate Bench](../gate-bench/) first if you haven't. This project uses three of the
same chips (CD4070, CD4081, CD4071) and answers the question every beginner asks: *how do
logic gates actually do math?*

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| **Binary addition** — $1 + 1 = 10_2$, column by column | Section 2 |
| **The Half Adder** — XOR for sum, AND for carry | Stage 1 |
| **XOR is addition without carry** — modulo-2 arithmetic | Section 2 |
| **The Full Adder** — two half adders and an OR gate to accept a carry-in | Stage 2 |
| **Mutually exclusive carries** — why a simple OR combines carries safely | Section 3 |
| **The Ripple-Carry Adder** — chaining bit columns right-to-left | Stage 2 |
| **Carry propagation delay** — why math takes time in silicon | Stage 3 |
| **ALUs and 64-bit CPUs** — why modern chips need carry-lookahead | Stage 3, and `.why` |

Total build time is about 2–2½ hours, in 3 stages you can stop between. Stopping after
Stage 1 leaves a fully working 1-bit Half Adder that can add $1 + 1$.

---

## Parts

Everything here is in the standard kit.

### Chips

All three chips share the exact same 14-pin quad layout, with **+ on pin 14** and **− on pin 7**.

| Chip | What it is | Gates used | Job in the adder |
|---|---|---|---|
| CD4070 | Quad 2-input XOR | 3 of 4 | Sum bits: Gate 1 for $S_0$, Gates 2 & 3 for $S_1$ |
| CD4081 | Quad 2-input AND | 3 of 4 | Carry bits: Gate 1 for $C_0$, Gates 2 & 3 for $C_1$ |
| CD4071 | Quad 2-input OR | 1 of 4 | Combines the two carries into $S_2$ (Carry Out) |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 4 | Tactile push buttons or slide switches | Two for number A ($A_1, A_0$), two for number B ($B_1, B_0$) |
| 4 | Resistor 100 kΩ | Pull-down resistors on the four input lines |
| 3 | LED 5 mm | Red or amber: $S_0$ (value 1), $S_1$ (value 2), $S_2$ (value 4) |
| 3 | Resistor 220 Ω (or 330 Ω) | Current-limiting resistors, one per LED |
| 3 | Capacitor 0.1 µF ceramic ("104") | Power decoupling, one right across pins 14 and 7 of each chip |
| 1 | Capacitor 47 µF or 100 µF electrolytic | Bulk smoothing across the power rails. Stripe marks negative |
| — | Solid-core hookup wire | 22 AWG, pre-cut or from a spool |

### Power

5 V from a breadboard power module or 4.5 V from 3 AA cells. Never connect this circuit to mains.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **The notch on a chip tells you which end is which.** Notch facing left → pin 1 bottom-left,
   numbers run anticlockwise to pin 14 at the top-left. Backwards power will destroy CMOS chips.
3. **Never leave an input dangling.** Every unused input goes straight to − (blue rail).
4. **Never wire an output straight to + or −.** That creates a dead short through the chip's internal FETs.
5. **Electrolytic capacitors have a polarity.** The stripe with minus signs marks the negative leg.
6. **Touch a metal table leg or radiator before handling chips.** Static electricity kills CMOS gates.
7. **Warm chip means stop.** Pull power immediately and check pin 14 (+) and pin 7 (−).

---

## Complete wire list

Written as *pin → pin*, never breadboard coordinates, so it works wherever you arrange your parts.
`+` is the red rail, `−` is the blue rail.

### Power rails and decoupling

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Supply + | Top red rail (+) | Main power |
| ☐ | Supply − | Top blue rail (−) | Main ground |
| ☐ | Top red rail | Bottom red rail | Link rails |
| ☐ | Top blue rail | Bottom blue rail | Link rails |
| ☐ | 100 µF capacitor | Across + and − rails | Bulk smoothing (stripe to −) |

### Chip power and tie-downs

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD4070 pin 14 | + rail | XOR power |
| ☐ | CD4070 pin 7 | − rail | XOR ground |
| ☐ | 0.1 µF capacitor | CD4070 pin 14 to pin 7 | Local decoupling |
| ☐ | CD4070 pin 12 | − rail | Tie unused Gate 4 input A |
| ☐ | CD4070 pin 13 | − rail | Tie unused Gate 4 input B |
| ☐ | CD4081 pin 14 | + rail | AND power |
| ☐ | CD4081 pin 7 | − rail | AND ground |
| ☐ | 0.1 µF capacitor | CD4081 pin 14 to pin 7 | Local decoupling |
| ☐ | CD4081 pin 12 | − rail | Tie unused Gate 4 input A |
| ☐ | CD4081 pin 13 | − rail | Tie unused Gate 4 input B |
| ☐ | CD4071 pin 14 | + rail | OR power |
| ☐ | CD4071 pin 7 | − rail | OR ground |
| ☐ | 0.1 µF capacitor | CD4071 pin 14 to pin 7 | Local decoupling |
| ☐ | CD4071 pin 5 | − rail | Tie unused Gate 2 input A |
| ☐ | CD4071 pin 6 | − rail | Tie unused Gate 2 input B |
| ☐ | CD4071 pin 8 | − rail | Tie unused Gate 3 input A |
| ☐ | CD4071 pin 9 | − rail | Tie unused Gate 3 input B |
| ☐ | CD4071 pin 12 | − rail | Tie unused Gate 4 input A |
| ☐ | CD4071 pin 13 | − rail | Tie unused Gate 4 input B |

### Four inputs (switches and pull-downs)

Each switch sits between `+` and an input row. A 100 kΩ resistor sits between that row and `−`.

| ✓ | Input line | Switch connection | Pull-down resistor | Meaning |
|---|---|---|---|---|
| ☐ | Line $A_0$ | Switch between + and line $A_0$ | 100 kΩ from line $A_0$ to − | Number A, Bit 0 (1s) |
| ☐ | Line $B_0$ | Switch between + and line $B_0$ | 100 kΩ from line $B_0$ to − | Number B, Bit 0 (1s) |
| ☐ | Line $A_1$ | Switch between + and line $A_1$ | 100 kΩ from line $A_1$ to − | Number A, Bit 1 (2s) |
| ☐ | Line $B_1$ | Switch between + and line $B_1$ | 100 kΩ from line $B_1$ to − | Number B, Bit 1 (2s) |

### Stage 1: Bit 0 (Half Adder)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Line $A_0$ | CD4070 pin 1 | Gate 1 input A (XOR) |
| ☐ | Line $A_0$ | CD4081 pin 1 | Gate 1 input A (AND) |
| ☐ | Line $B_0$ | CD4070 pin 2 | Gate 1 input B (XOR) |
| ☐ | Line $B_0$ | CD4081 pin 2 | Gate 1 input B (AND) |
| ☐ | CD4070 pin 3 (XOR 1 OUT) | $S_0$ LED anode (long leg) | Bit 0 Sum output |
| ☐ | $S_0$ LED cathode (short leg) | 220 Ω resistor to − rail | Sum 0 current limiter |
| ☐ | CD4081 pin 3 (AND 1 OUT) | *(In Stage 1: carry test LED; in Stage 2: feeds Bit 1)* | Bit 0 Carry Out ($C_0$) |

### Stage 2: Bit 1 (Full Adder) and Ripple Carry

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Line $A_1$ | CD4070 pin 5 | Gate 2 input A (XOR) |
| ☐ | Line $A_1$ | CD4081 pin 5 | Gate 2 input A (AND) |
| ☐ | Line $B_1$ | CD4070 pin 6 | Gate 2 input B (XOR) |
| ☐ | Line $B_1$ | CD4081 pin 6 | Gate 2 input B (AND) |
| ☐ | CD4070 pin 4 (XOR 2 OUT) | CD4070 pin 8 | Gate 3 input A (XOR): intermediate sum |
| ☐ | CD4070 pin 4 (XOR 2 OUT) | CD4081 pin 8 | Gate 3 input A (AND): intermediate sum |
| ☐ | CD4081 pin 3 ($C_0$ Carry) | CD4070 pin 9 | Gate 3 input B (XOR): carry from Bit 0 |
| ☐ | CD4081 pin 3 ($C_0$ Carry) | CD4081 pin 9 | Gate 3 input B (AND): carry from Bit 0 |
| ☐ | CD4070 pin 10 (XOR 3 OUT) | $S_1$ LED anode | Bit 1 Sum output (2s place) |
| ☐ | $S_1$ LED cathode | 220 Ω resistor to − rail | Sum 1 current limiter |
| ☐ | CD4081 pin 4 (AND 2 OUT) | CD4071 pin 1 | Gate 1 input A (OR): carry from $A_1 \cdot B_1$ |
| ☐ | CD4081 pin 10 (AND 3 OUT) | CD4071 pin 2 | Gate 1 input B (OR): carry from intermediate sum $\cdot C_0$ |
| ☐ | CD4071 pin 3 (OR 1 OUT) | $S_2$ LED anode | Bit 2 Sum / Carry Out (4s place) |
| ☐ | $S_2$ LED cathode | 220 Ω resistor to − rail | Sum 2 current limiter |

---

## Pin reference

Verified against Texas Instruments datasheets: CD4070B (SCHS055E), CD4081B (SCHS057C), and CD4071B (SCHS056D).

All three chips use the standard CMOS quad 2-input gate pinout:

```
CD4070 quad XOR       CD4081 quad AND       CD4071 quad OR
  gate 1   in  1,  2  ->  OUT  3          + VDD on pin 14
  gate 2   in  5,  6  ->  OUT  4          − VSS on pin  7
  gate 3   in  8,  9  ->  OUT 10
  gate 4   in 12, 13  ->  OUT 11
```

> **Watch out:** Gates 2 and 3 are numbered the other way up from gates 1 and 4. Output pin 4
> sits *above* input pin 5, and output pin 10 sits *below* input pin 9. Look twice before pushing
> a wire in.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights on any switch setting | Power is not reaching pin 14 (+) and pin 7 (−) on one or more chips. Measure with a multimeter or check every red and blue wire. |
| A chip gets hot | Power or ground is backwards, or an output pin is wired straight to a power rail. **Unplug immediately.** |
| Lamps flicker when hands are near the board | A dangling input. Every switch must have a 100 kΩ pull-down resistor to −, and all unused gate inputs must be tied to −. |
| An LED never lights up | The LED is backwards (long leg must go toward the chip output), or plugged into the wrong breadboard row. |
| $1 + 1$ gives $S_0$ lit instead of dark | You wired the sum to the AND gate instead of the XOR gate, or swapped pins 3 and 4. |
| $2 + 2$ gives $S_1$ lit and $S_2$ dark | The carry from Bit 1 did not reach the OR gate, or the OR gate inputs (pins 1 and 2) are not connected to the AND outputs. |
| Adding $1 + 1$ produces $S_1$ lit, but adding $2 + 1$ does nothing | The ripple carry wire from CD4081 pin 3 to CD4070 pin 9 / CD4081 pin 9 is loose or in the wrong column. |
| Everything looks wrong at once | Unplug power. Take a five-minute break. Verify chip pin 1 is at the notch for all three chips, then trace one wire at a time against the wire list. |
