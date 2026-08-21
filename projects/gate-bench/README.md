# The Gate Bench

One little circuit, six different chips, and a guessing game at the end.

You wire up two switches and three lights — once — and then swap logic chips through it.
Each chip has a different opinion about your two switches. By the last stage you can work
out which chip somebody plugged in while you weren't looking, in three tests.

Built for a curious 11-year-old, using CD4000-series logic chips, a breadboard, five LEDs
and no transistors at all.

**Open [`guide.html`](guide.html) in a browser** — that's the real guide, with diagrams and
a working bench simulator you can play with before you touch a wire. This file is the bench
reference: parts, wire lists, troubleshooting.

This is the gentle introduction to [the Logic Vault](../logic-vault/), which uses the same
chips to build a combination safe.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| A wire is either 1 or 0 (voltage or no voltage) | Every stage |
| A truth table *is* the whole specification of a chip | Stages 1–4 |
| AND, OR, XOR, NAND, NOR, NOT | One stage each, one chip each |
| The circle on a symbol means "and then flip it" | Stage 3 |
| A NAND with its inputs tied together becomes a NOT | Stage 3 |
| Five different chips can share one pinout — and why they do | Section 4 |
| Logic chips can *think* but not *push* | Stage 1, and the bonus transistor |
| A floating input is not 0, and why buttons need pull-down resistors | Stage 5 |
| Two NOTs in a row are a buffer, not a waste | Stage 4 |
| NAND alone can build every other gate (De Morgan) | Bonus 1 |
| Choosing the test that halves the field | Stage 5, the guessing game |

Total build time is about 1½–2 hours, in five stages you can stop between. Only the first
stage involves real wiring.

---

## Parts

Everything here is in the kit.

### Chips — one on the board at a time

| Chip | What it is | Meets you in |
|---|---|---|
| CD4081 | Quad 2-input AND | Stage 1, Stage 5 |
| CD4071 | Quad 2-input OR | Stage 2 |
| CD4070 | Quad 2-input XOR | Stage 2, Stage 5 |
| CD4011 | Quad 2-input NAND | Stage 3, bonus |
| CD4001 | Quad 2-input NOR | Stage 3 |
| CD4069 | Hex NOT | Stage 4 |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 2 | Yellow LED | The A and B lamps |
| 1 | Red LED | The output lamp |
| 1 | Green LED | Stage 5 — the GO light |
| 2 | 1 kΩ resistor | The two input lamps |
| 2 | 220 Ω resistor | Output lamp, and the GO light |
| 2 | 10 kΩ resistor | Stage 5 — button pull-downs |
| 2 | Push button (small) | Stage 5 — the two hands |
| 1 | 0.1 µF ceramic ("104") | Across the chip's power pins |
| 1 | 100 µF electrolytic | Across the rails — **stripe goes to −** |
| 1 | Breadboard | Half-size is plenty |
| ~20 | Jumper wires | Red for +, black for −, colours for signals |

The bonus stage adds **1 PN2222 transistor**, **1 white LED** and **1 more 10 kΩ**.

### Power

**4.5 V to 5 V.** Either three AA cells, or the MB102 breadboard power module set to 5 V.

These chips are happy anywhere from 3 V to 18 V, so nothing here is fragile about voltage.
Nothing in this project touches mains electricity.

---

## Rules for not breaking things

1. **Unplug the power before you swap a chip or move a wire.** You will swap chips five
   times today. A live swap is the one that kills a chip.
2. **The notch on a chip tells you which end is which.** Notch on the left → pin 1 is
   bottom-left, and pin numbers run anticlockwise. Put a chip in backwards and pin 14 gets
   ground while pin 7 gets +5 V; the chip gets hot and dies.
3. **Never leave an input wire dangling.** A CMOS input connected to nothing picks up
   radio noise and flickers randomly. Every input goes to + or to − or to another chip's
   output. Unused inputs go to −.
4. **Never wire an output straight to + or −.** That's a short circuit through the chip.
   This bites hardest in Stage 4: the holes you ground for the quad chips are **outputs**
   on the CD4069.
5. **The electrolytic capacitor has a polarity.** The stripe down one side marks the
   negative leg. Backwards, it can pop.
6. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
   Hold chips by the ends, not the legs.
7. If a chip ever feels **warm**, pull the power immediately and check rules 2 and 4.

---

## The bench — built once, in Stage 1

Everything is written as *pin → pin*, never as breadboard coordinates, so it works no
matter where you place things. `+` means the red rail, `−` means the blue/black rail.

Pick two empty columns and call them the **A column** and the **B column**. Everything to
do with input A meets in its column.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |
| ☐ | 100 µF + leg | Red rail (striped leg to blue rail) |

### The chip

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | The three spare gates' inputs |

### The two inputs

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A column | pin 1 | Input A |
| ☐ | A column | loose jumper, free end | The A switch — plugs into + or − |
| ☐ | B column | pin 2 | Input B |
| ☐ | B column | loose jumper, free end | The B switch |

### The three lamps

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A column | 1 kΩ → yellow LED long leg | A lamp |
| ☐ | Yellow LED short leg | − | |
| ☐ | B column | 1 kΩ → yellow LED long leg | B lamp |
| ☐ | Yellow LED short leg | − | |
| ☐ | pin 3 | 220 Ω → red LED long leg | Output lamp |
| ☐ | Red LED short leg | − | |

That's the whole bench: about twenty wires, and you never rebuild it.

---

## What changes for each chip

| Stage | Chip | What you change |
|---|---|---|
| 1 | CD4081 (AND) | Nothing — this is the bench as built |
| 2 | CD4071 (OR) | **Nothing.** Swap the chip, same holes |
| 2 | CD4070 (XOR) | **Nothing** |
| 3 | CD4011 (NAND) | **Nothing** |
| 3 | CD4001 (NOR) | **Nothing** |
| 3 | CD4011 as a NOT | Add one wire: A column → pin 2. Park the B jumper in − |
| 4 | CD4069 (NOT) | See below — the one real rewire |
| 5 | CD4081 + buttons | Buttons and pull-downs replace the loose jumpers |
| 5 | CD4070 stair light | Swap the chip, put the loose jumpers back |

### Stage 4 — the CD4069 rewire

> **Pull the six ground jumpers out before this chip goes in.** On the quad chips, pins 5,
> 6, 8, 9, 12 and 13 are all inputs, and grounding them is correct. On the CD4069, pins
> **6, 8 and 12 are outputs**. Leaving those jumpers in place shorts three outputs to
> ground.

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Remove | the six jumpers on pins 5, 6, 8, 9, 12, 13 | Three would ground an output |
| ☐ | Move the output lamp | from pin 3 to **pin 2** | Gate 1's output is pin 2 here |
| ☐ | A column | pin 1 | Already there — leave it |
| ☐ | pins 3, 5, 9, 11, 13 | − | The five unused *inputs* |
| ☐ | B jumper | park the free end in − | Nothing for B to do |

Then, for two inverters in a row:

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Remove | the jumper grounding pin 3 | Pin 3 carries a signal now |
| ☐ | pin 2 | pin 3 | First NOT feeds the second |
| ☐ | Move the output lamp | from pin 2 to **pin 4** | Watch the second gate |

---

## Stage 5 wiring

### The two-hand interlock — CD4081

Restore the bench to its Stage 1 state first: six ground jumpers back in, output lamp back
on pin 3.

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Button 1 leg | + | |
| ☐ | Button 1 leg, **diagonally opposite** | A column | |
| ☐ | A column | 10 kΩ → − | Pull-down |
| ☐ | Button 2 leg | + | |
| ☐ | Button 2 leg, **diagonally opposite** | B column | |
| ☐ | B column | 10 kΩ → − | Pull-down |
| ☐ | pin 3 | 220 Ω → green LED long leg | GO light |
| ☐ | Green LED short leg | − | |

A 4-pin tactile button has its legs joined in pairs. Using diagonally opposite legs is the
one choice that is always right.

The pull-downs are not optional. An unpressed button connects its input to *nothing*, not
to 0 — rule 3. The 10 kΩ holds the input at 0 while the button is up, and is weak enough
that pressing the button overrules it.

### The stair light — CD4070

Swap the CD4081 for the CD4070, take the buttons out, and put the two loose jumpers back.
Move either jumper between + and − and the lamp changes state, every time, whichever
jumper you touch. That is how a staircase with a switch at each end is wired.

---

## Bonus wiring

### 1. AND out of NANDs — CD4011

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A column | pin 1 | Gate 1 input |
| ☐ | B column | pin 2 | Gate 1 input |
| ☐ | pin 3 | pin 5 | Gate 1's answer into gate 2 |
| ☐ | pin 3 | pin 6 | Gate 2's inputs tied together — a NOT |
| ☐ | Output lamp | on pin 4 | Gate 2's output |
| ☐ | pins 8, 9, 12, 13 | − | The two spare gates |

### 2. OR out of NANDs — CD4011

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | A column | pins 5 **and** 6 | Gate 2 becomes NOT A |
| ☐ | B column | pins 8 **and** 9 | Gate 3 becomes NOT B |
| ☐ | pin 4 | pin 1 | NOT A into gate 1 |
| ☐ | pin 10 | pin 2 | NOT B into gate 1 |
| ☐ | Output lamp | on pin 3 | Gate 1's output |
| ☐ | pins 12, 13 | − | The one spare gate |

`NAND(NOT A, NOT B)` is `A OR B`. That's De Morgan's law, built out of wire.

### 3. A bright lamp — PN2222

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Gate output pin | 10 kΩ → base (middle leg) | About 0.4 mA — all the chip can spare |
| ☐ | Emitter (left leg) | − | |
| ☐ | + | 220 Ω → white LED long leg | Current off the rail, not the chip |
| ☐ | White LED short leg | Collector (right leg) | |

PN2222 with the flat side toward you and the legs down: **E – B – C**.

---

## Why every lamp is dim

A CD4000 output at 5 V behaves like a 5 V source with roughly a kilohm of resistance built
in. It can push about 3 mA before its voltage sags noticeably, and the datasheet only
promises 0.51 mA at a nearly-full 4.6 V out. So:

- The **output lamp** draws about 2.6 mA. The 220 Ω resistor is barely doing anything —
  the chip itself is the limit. It stays in because it's the right habit and because it
  protects the LED when the same wire is later driven from a rail.
- The **input lamps** are driven straight from the rails, where 220 Ω would give about
  14 mA and make them five times brighter than the output. The 1 kΩ resistors hold them
  back to about 3 mA so all three lamps match. A bright lamp beside a dim one reads as a
  fault; matching them is worth two resistors.
- The **bonus transistor** takes about 0.4 mA of base current from the chip and passes
  about 8 mA through a white LED — roughly thirty times what the chip could manage alone.

None of this is a defect. These are 1968 designs meant to talk to other chips, not to
light rooms.

---

## Pin reference

All six verified against the Texas Instruments datasheets. Pin 14 is always +, pin 7 is
always −, on every chip here.

```
CD4081 quad AND        CD4071 quad OR         CD4070 quad XOR
CD4011 quad NAND       CD4001 quad NOR
 in 1,  2  -> out  3      ... all five of these chips share
 in 5,  6  -> out  4          one identical pinout, so this
 in 8,  9  -> out 10          block describes all of them
 in 12,13  -> out 11

CD4069  hex NOT
 in  1 -> out  2
 in  3 -> out  4
 in  5 -> out  6
 in  9 -> out  8      <- note: the numbers run backwards
 in 11 -> out 10         from here on
 in 13 -> out 12
```

Learn the quad layout once and you've learned five chips. The CD4069 is the exception, and
the one that can burn a chip if you assume otherwise.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights at all | Power isn't reaching pin 14 and pin 7. Check both, with the chip in. |
| A chip gets warm | Power in backwards, or a jumper grounding an output. Unplug now. |
| Yellow lamps fine, red never lights | Output lamp on the wrong pin, or in backwards. Long leg toward the resistor. |
| Red lamp on for all four rows | Both jumpers are landing in the same column, or a column isn't reaching the pin you think. |
| Lamps flicker or change on their own | A floating input. Find the input with nothing on it and tie it to −. |
| The table you measured matches no gate | Two rows are probably swapped. Redo it, saying each jumper position out loud. |
| It worked, then stopped after a swap | A leg is bent under the chip instead of in its hole. Lift it and look along the legs at eye level. |
| Everything is wrong at once | Unplug, walk away for five minutes, come back and re-read one table. This is what real engineers do. |

The technique worth learning: don't stare at the whole board. Pick one signal — say A —
and follow it, testing each step: jumper, column, pin, lamp. Halve the problem, then halve
it again.

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: diagrams, five build stages, live bench simulator |
| [`worksheet.md`](worksheet.md) | Six truth tables to fill in, the counting exercises, the guessing-game log |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
