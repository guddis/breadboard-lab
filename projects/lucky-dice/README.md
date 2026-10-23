# Lucky Dice

Hold a button and seven LEDs flicker through the faces of a die. Let go and it stops on one.

There is no computer in it and no random-number chip. Three flip-flops pass a bit along a
row, and one gate decides what the next bit is. The sequence jumps about so much that your
thumb cannot predict where it will stop — and the build shows exactly why it is only
*almost* random.

Built for a curious 11-year-old and up, using CD4000-series logic chips, a breadboard and a
handful of LEDs.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/lucky-dice/guide.html) in a browser** — that's the real guide, and the die is
rollable on the page before you build anything. This file is the bench reference: parts,
wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| A shift register: each tick, every bit copies its neighbour | Stage 2 |
| Feeding a register's output back into its input makes a sequence | Stage 3 |
| XNOR asks "are these the same?" — and picks which state is the trap | Stage 3 |
| A circuit can have a state it cannot leave, and RESET is the way out | Stage 3, Section 3 |
| Three bits give eight states; the best feedback uses seven | Section 2 |
| Handing out the faces cleverly turns a decoder into two gates | Section 4, Stage 4 |
| A CD4000 output is for logic; a transistor is for lamps | Stage 4 |
| Seven outcomes cannot be shared fairly among six faces — reject and roll again | Section 8 |
| "Random" in electronics means "too fast to steer" | Stage 4, worksheet |

Total build time is about 2 hours, in four stages you can stop between.

---

## Parts

### Chips

| Chip | What it is | Job in the die |
|---|---|---|
| CD4093 | Quad 2-input NAND, Schmitt inputs | The clock — gate 1 with its inputs tied |
| CD4081 | Quad 2-input AND | Gate 1: clock only while ROLL is held. Gate 2: pip signal **c** |
| CD4013 × 2 | Dual D flip-flop | Three of the four flip-flops are the register; the fourth sits idle |
| CD4077 | Quad 2-input XNOR | The feedback |
| CD4071 | Quad 2-input OR | Pip signal **a** |
| CD4070 | Quad 2-input XOR | Stage 3 experiment only — swapped in for the CD4077 and back |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 7 | LED, all one colour | The pips. White or yellow looks most like a die. Three double as test lamps in Stages 1–3 |
| 4 | PN2222 NPN transistor | One per pip signal. Flat side toward you, legs down: **E – B – C** |
| 2 | Push button (small) | ROLL and RESET |
| 7 | 330 Ω resistor | One per pip |
| 3 | 2 kΩ resistor | Test lamps in Stages 1–3, removed in Stage 4 |
| 6 | 10 kΩ resistor | Two button pull-downs, four transistor bases |
| 1 | 100 kΩ resistor | Clock timing |
| 1 | 10 µF electrolytic | Slow clock for building — **stripe goes to −** |
| 7 | 0.1 µF ceramic ("104") | One per chip across its power pins (six), plus one for the fast clock |
| 1 | 100 µF electrolytic | Across the power rails — **stripe goes to −** |
| 1 | Breadboard | Full-size. Six chips and seven LEDs need the room |
| ~60 | Jumper wires | Red for +, black for −, colours for signals |

The bonus "roll-again" lamp needs one more PN2222, one 10 kΩ, one 330 Ω and one green LED.
The kit has five PN2222, so it fits.

### Power

**4.5 V to 5 V.** Either three AA cells, or the MB102 breadboard power module set to 5 V.

All six chips are happy anywhere from 3 V to 18 V. Nothing in this project touches mains
electricity.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **All six chips are 14-pin: + on pin 14, − on pin 7.** Notch to the left → pin 1 is
   bottom-left, and pin numbers run anticlockwise. Backwards means power and ground swap,
   and the chip gets hot and dies. There is no 16-pin chip in this project.
3. **Never leave an input wire dangling.** That includes the SET and RESET pins you are not
   using and every spare gate input. Unused inputs go to −.
4. **Press RESET after every power-up.** A flip-flop wakes up holding anything, and one of
   the eight states is a trap (111) that ROLL cannot leave.
5. **Never wire an output straight to + or −.** That's a short circuit through the chip.
6. **The electrolytic capacitors have a polarity.** The stripe marks the negative leg.
   Backwards, they can pop. The little "104" ceramics don't care.
7. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
8. If a chip ever feels **warm**, pull the power immediately and check rule 2.

---

## Complete wire list

Everything is written as *pin → pin*, never as breadboard coordinates, so it works no
matter where you place things. `+` means the red rail, `−` means the blue/black rail.

Name the two CD4013 chips **A** and **B**. Chip A holds Q1 (half 1) and Q2 (half 2). Chip B
holds Q3 (half 1); its half 2 is idle.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |
| ☐ | 100 µF + leg | Red rail (stripe/− leg to blue rail) |

### Stage 1 — CD4093, the clock

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | pin 1 | pin 2 | Both inputs together: a NOT gate |
| ☐ | 100 kΩ | pin 3 → pin 1 | Output back to its own input |
| ☐ | 10 µF | pin 1 → − (stripe to −) | Slow clock for building |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | Three unused gates |
| ☐ | pin 3 | 2 kΩ → LED long leg; short leg → − | Clock lamp. **Remove at the start of Stage 2** |

Output: **pin 3 = RAW CLOCK**. Leave pins 4, 10 and 11 unconnected — they are outputs of
unused gates.

### Stage 2 — CD4081, the clock switch

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | CD4093 pin 3 | pin 1 | The raw clock |
| ☐ | ROLL node | pin 2 | Permission to run |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | Spare for now — pins 5 and 6 move in Stage 4 |

Output: **pin 3 = CLK**. Leave pins 4, 10 and 11 unconnected for now.

### The two buttons

A 4-pin tactile button has its legs joined in hidden pairs. Using **diagonally opposite**
legs is the one choice that is always right.

| ✓ | From | To |
|---|---|---|
| ☐ | ROLL leg | + |
| ☐ | ROLL leg, **diagonally opposite** | ROLL node |
| ☐ | ROLL node | 10 kΩ → − |
| ☐ | ROLL node | CD4081 pin 2 |
| ☐ | RESET leg | + |
| ☐ | RESET leg, **diagonally opposite** | RESET node |
| ☐ | RESET node | 10 kΩ → − |
| ☐ | RESET node | A pin 4, A pin 10, B pin 4 |

The 10 kΩ pull-downs are not optional. Without them the node is connected to nothing when
the button is up, and the register will run — or clear — as you walk past.

### Stage 2 — CD4013 × 2, the register

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A and B, pin 14 | + | Power |
| ☐ | A and B, pin 7 | − | Ground |
| ☐ | 0.1 µF on each | between pin 14 and pin 7 | |
| ☐ | A pin 3, A pin 11, B pin 3 | CLK (CD4081 pin 3) | All three share one clock |
| ☐ | A pin 1 (Q1) | A pin 9 (D2) | Q1 passes to Q2 |
| ☐ | A pin 13 (Q2) | B pin 5 (D) | Q2 passes to Q3 |
| ☐ | A pin 5 (D1) | + | **Temporary.** Becomes the feedback in Stage 3 |
| ☐ | A pins 6, 8; B pin 6 | − | SET unused |
| ☐ | B pins 8, 9, 10, 11 | − | The idle half |

Outputs: **A pin 1 = Q1**, **A pin 13 = Q2**, **B pin 1 = Q3**. Leave A pins 2 and 12 and
B pins 2, 12 and 13 unconnected — they are the inverted outputs.

Test lamps for Stages 2 and 3: **2 kΩ → LED → −** on A pin 1, A pin 13 and B pin 1.
Use 2 kΩ, not 330 Ω: each Q also feeds the next flip-flop and has to stay a clean 1.

### Stage 3 — CD4077, the feedback

Remove the wire from A pin 5 to +.

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | A pin 13 (Q2) | pin 1 | First tap |
| ☐ | B pin 1 (Q3) | pin 2 | Second tap |
| ☐ | pin 3 | A pin 5 (D1) | The new bit enters the front |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | Unused gates |

For the experiment, pull the CD4077 and put a **CD4070** in the same holes. Same pinout.
Put the CD4077 back afterwards.

### Stage 4 — CD4071 and CD4081 gate 2, the decoder

Remove the three test lamps and their 2 kΩ resistors.

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD4071 pin 14 | + | Power |
| ☐ | CD4071 pin 7 | − | Ground |
| ☐ | 0.1 µF | between CD4071 pin 14 and pin 7 | |
| ☐ | A pin 13 (Q2) | CD4071 pin 1 | |
| ☐ | B pin 1 (Q3) | CD4071 pin 2 | |
| ☐ | CD4071 pins 5, 6, 8, 9, 12, 13 | − | Unused gates |
| ☐ | A pin 13 (Q2) | CD4081 pin 5 | Move off −. Gate 2 now computes Q2 AND Q3 |
| ☐ | B pin 1 (Q3) | CD4081 pin 6 | Move off − |

The four signals:

| Signal | Comes from | Lights these pips |
|---|---|---|
| **a** = Q2 OR Q3 | CD4071 pin 3 | top-left, bottom-right |
| **b** = Q3 | B pin 1 | top-right, bottom-left |
| **c** = Q2 AND Q3 | CD4081 pin 4 | middle-left, middle-right |
| **C** = Q1 | A pin 1 | centre |

### Stage 4 — four pip drivers

Build this **once per signal** — four times:

| ✓ | From | To |
|---|---|---|
| ☐ | The signal | 10 kΩ → transistor base (middle leg) |
| ☐ | Transistor emitter (left leg) | − |
| ☐ | + | 330 Ω → LED long leg — **one 330 Ω per LED** |
| ☐ | LED short leg(s) | Transistor collector (right leg) |

Signals **a**, **b** and **c** each drive two LEDs: two 330 Ω, two LEDs, one transistor.
Signal **C** drives one.

The reason is current, not decoration. Each lit LED draws about 8 mA, and a CD4000 output
gives a milliamp or so. Q1, Q2 and Q3 also have to feed the next flip-flop and the gates
as clean logic levels. Through 10 kΩ into a base the output only gives 0.4 mA — a clean 1
for the logic, a bright lamp for the pip.

### Stage 4 — the fast clock

Power off. Replace the 10 µF (pin 1 → −) with a **0.1 µF**. The 100 kΩ stays.

### Bonus — "roll again" lamp

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A pin 1 (Q1) | CD4071 pin 5 | Move off − |
| ☐ | CD4071 pin 3 (a) | CD4071 pin 6 | Move off − |
| ☐ | CD4071 pin 4 | Fifth driver: 10 kΩ → PN2222 base, 330 Ω → green LED | Lit means "valid roll" |

CD4071 pin 4 is Q1 OR Q2 OR Q3: 1 for every state except dark.

### Bonus — four bits

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | B pin 9 (D2) | B pin 1 (Q3) | Move off − |
| ☐ | B pin 11 | CLK | Move off − |
| ☐ | B pin 10 | RESET node | Move off − |
| ☐ | B pin 1 (Q3) | CD4077 pin 1 | Move from Q2. First tap is now Q3 |
| ☐ | B pin 13 (Q4) | CD4077 pin 2 | Move from Q3. Second tap is now Q4 |

Output: **B pin 13 = Q4**. The cycle becomes 15 states. The die decoder no longer means
anything; put test lamps on all four and count.

---

## Clock speeds

The timing resistor sits between CD4093 pin 3 and pin 1; the capacitor between pin 1 and −.

| Resistor | Capacitor | Ticks per second | Use |
|---|---|---|---|
| 100 kΩ | 10 µF | ≈ 1.2 | Building and watching the bits move |
| 100 kΩ | 0.1 µF | ≈ 120 | Rolling — 17 trips round the seven states a second |

The formula is **f ≈ 1.23 ÷ (R × C)**, the same one as the Reaction Machine, because the
CD4093 has the same kind of two-threshold input. Expect your own build to land anywhere
within about 30 % of the table; electrolytic capacitors are allowed to be 20 % out and the
thresholds vary between chips. Nothing here cares.

---

## The state sequence

With the CD4077 fitted, from RESET (000):

| Tick | Q1 Q2 Q3 | Face |
|---|---|---|
| 0 | 0 0 0 | dark — roll again |
| 1 | 1 0 0 | 1 |
| 2 | 1 1 0 | 3 |
| 3 | 0 1 1 | 6 |
| 4 | 1 0 1 | 5 |
| 5 | 0 1 0 | 2 |
| 6 | 0 0 1 | 4 |
| 7 | 0 0 0 | back to the start |

The eighth state, 111, feeds itself and never leaves. With a CD4070 instead, the trap is
000 — exactly where RESET puts you.

---

## Pin reference

Checked against the Texas Instruments datasheets: CD4013B (SCHS023E), CD4077B (SCHS055E),
CD4070B, CD4081B (SCHS057C), CD4071B (SCHS056D), CD4093B (SCHS115D).

```
CD4013  dual D flip-flop          CD4093 / CD4081 / CD4077 / CD4071 / CD4070
 1 Q1        14 +VDD               all the same layout
 2 Q1-not    13 Q2                  in  1,  2 -> out  3
 3 CLOCK1    12 Q2-not              in  5,  6 -> out  4
 4 RESET1    11 CLOCK2              in  8,  9 -> out 10
 5 D1        10 RESET2              in 12, 13 -> out 11
 6 SET1       9 D2                  +VDD = 14   -VSS = 7
 7 -VSS       8 SET2
```

The CD4013 triggers on the **rising** clock edge. Half 1 uses pins 1–6; half 2 uses 8–13,
and the two halves are laid out as mirror images of each other, so Q is pin 1 for half 1
but pin 13 for half 2.

| Flip-flop | Q | D | CLOCK | RESET | SET |
|---|---|---|---|---|---|
| Q1 — chip A, half 1 | 1 | 5 | 3 | 4 | 6 |
| Q2 — chip A, half 2 | 13 | 9 | 11 | 10 | 8 |
| Q3 — chip B, half 1 | 1 | 5 | 3 | 4 | 6 |
| idle — chip B, half 2 | 13 | 9 | 11 | 10 | 8 |

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights at all | Power not reaching a chip. All six want + on pin 14 and − on pin 7. |
| A chip gets warm | Power in backwards, or an output wired to a rail. Unplug now. |
| Clock lamp stays on or off | The 100 kΩ must go from pin 3 **back to pin 1**, and pins 1 and 2 must be tied. |
| Clock lamp glows steadily instead of blinking | It's running fast — that's a 0.1 µF. Fit the 10 µF for building. |
| Register never moves | CD4081 pin 2 isn't reaching the ROLL node, or pin 3 isn't reaching all three clock pins (A 3, A 11, B 3). |
| Register runs when you aren't holding ROLL | The ROLL node's 10 kΩ pull-down is missing. |
| All lamps lit and ROLL does nothing | You powered on inside the 111 trap. Press RESET. |
| All dark and ROLL does nothing | A CD4070 (XOR) is fitted instead of the CD4077, or the feedback wire to A pin 5 is missing. |
| RESET leaves one bit alone | That bit's reset pin: A pin 4, A pin 10 or B pin 4. |
| Pattern is wrong but repeats | Q2 and Q3 swapped on the XNOR, or a Q wired to the wrong D. |
| Test lamps are dim | Normal. 2 kΩ keeps each Q a clean logic 1. |
| Test lamps bright, pattern erratic | A lamp is on the output without its 2 kΩ, dragging it to a vague voltage. |
| One pair of pips never lights | That transistor is in backwards. Flat side toward you: E – B – C. |
| One pip in a pair never lights | That LED is backwards, or its 330 Ω leg isn't in the right column. |
| Faces look wrong: pairs on the wrong sides | Pips swapped between two groups. Check the signal table. |
| Dark die about one roll in seven | Normal. That is the seventh state. Roll again. |
| Everything is wrong at once | Unplug, walk away for five minutes, come back and re-read one table. This is what real engineers do. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: four stages, and the die rollable in the browser |
| [`worksheet.md`](worksheet.md) | Clock measurements, the sequence, the trap, the six-every-time trick and a 60-roll tally |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
